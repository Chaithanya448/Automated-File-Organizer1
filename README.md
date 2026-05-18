# Automated-File-Organizer1
import os
import shutil

# Folder path to organize
SOURCE_FOLDER = "sample_files"

# File type categories
FILE_CATEGORIES = {
    "Images": [".jpg", ".jpeg", ".png", ".gif"],
    "Documents": [".pdf", ".docx", ".txt", ".pptx"],
    "Videos": [".mp4", ".mkv", ".avi"],
    "Music": [".mp3", ".wav"],
    "Archives": [".zip", ".rar"],
    "Python_Files": [".py"]
}

def organize_files():
    # Check if source folder exists
    if not os.path.exists(SOURCE_FOLDER):
        print(f"Folder '{SOURCE_FOLDER}' does not exist.")
        return

    # Loop through all files in source folder
    for file_name in os.listdir(SOURCE_FOLDER):
        file_path = os.path.join(SOURCE_FOLDER, file_name)

        # Skip folders
        if os.path.isdir(file_path):
            continue

        # Get file extension
        _, extension = os.path.splitext(file_name)

        moved = False

        # Check category
        for folder_name, extensions in FILE_CATEGORIES.items():
            if extension.lower() in extensions:

                # Create category folder if not exists
                destination_folder = os.path.join(SOURCE_FOLDER, folder_name)
                os.makedirs(destination_folder, exist_ok=True)

                # Move file
                shutil.move(file_path, os.path.join(destination_folder, file_name))

                print(f"Moved: {file_name} --> {folder_name}")
                moved = True
                break

        # Move unknown files
        if not moved:
            other_folder = os.path.join(SOURCE_FOLDER, "Others")
            os.makedirs(other_folder, exist_ok=True)

            shutil.move(file_path, os.path.join(other_folder, file_name))
            print(f"Moved: {file_name} --> Others")

# Run program
organize_files()

print("\nFile organization completed successfully!")
print("Intern ID: CITS1138")
