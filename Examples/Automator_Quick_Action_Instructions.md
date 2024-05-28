
# Creating an Automator Quick Action to Execute a Bash Script

To create an Automator Quick Action that executes your bash script inside the selected folder, follow these steps:

1. **Open Automator:**
   - Open Automator from the Applications folder or by searching for it in Spotlight.

2. **Create a New Document:**
   - Choose "Quick Action" as the document type.

3. **Configure Workflow Receives:**
   - Set "Workflow receives current" to "folders" in "Finder".

4. **Add a Run Shell Script Action:**
   - In the left pane, search for "Run Shell Script" and drag it to the workflow area on the right.

5. **Configure the Shell Script:**
   - Set "Pass input" to "as arguments".
   - Replace the default script with the following:

    ```bash
    for folder in "$@"
    do
      # Get the directory where the script is located
      script_dir="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

      # Folder to search for files (use the selected folder)
      input_folder="$folder"

      # Output file (place in the selected folder)
      output_file="$input_folder/full_source_code.txt"

      # Add file types to search for
      file_types=("*.swift" "*.h" "*.m" "*.xib" "*.storyboard")

      # Add any folder to ignore here
      ignored_folders=("Pods")

      # Clear the output file if it exists
      > "$output_file"

      # Build the find command dynamically
      find_command="find "$input_folder""

      for ignored_folder in "${ignored_folders[@]}"; do
        find_command+=" -name '$ignored_folder' -prune -o"
      done

      find_command+=" \( "
      for ((i=0; i<${#file_types[@]}; i++)); do
        find_command+=" -name '${file_types[$i]}'"
        if [ $i -lt $((${#file_types[@]} - 1)) ]; then
          find_command+=" -o"
        fi
      done
      find_command+=" \) -print0"

      # Execute the find command and process files
      eval $find_command | while IFS= read -r -d '' file; do
        # Add a header for each file with its full path
        echo "### File: $(realpath "$file") ###" >> "$output_file"
        # Append the contents of the file
        cat "$file" >> "$output_file"
        # Add a separator between files
        echo -e "\n\n" >> "$output_file"
      done
    done
    ```

6. **Save the Quick Action:**
   - Save the Quick Action with a meaningful name, such as "AI Ready - iOS".

Now, you can use this Quick Action from the Finder. Right-click any folder, go to the "Quick Actions" menu, and select the name of your Quick Action. It will execute the script inside the selected folder and create the `full_source_code.txt` file with the concatenated source files.

Let me know if you need any more assistance!
