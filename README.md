import os
import shutil

def organize_folder(target_path):
    # File types ki categories
    extensions = {
        "Images": [".jpg", ".jpeg", ".png", ".gif", ".svg"],
        "Documents": [".pdf", ".docx", ".txt", ".xlsx", ".pptx"],
        "Videos": [".mp4", ".mkv", ".mov"],
        "Music": [".mp3", ".wav"],
        "Archives": [".zip", ".tar", ".rar"],
        "Scripts": [".py", ".js", ".cpp", ".html"]
    }

    if not os.path.exists(target_path):
        print("Path sahi nahi hai!")
        return

    for filename in os.listdir(target_path):
        filepath = os.path.join(target_path, filename)

        # Agar folder hai toh skip karein
        if os.path.isdir(filepath):
            continue

        file_ext = os.path.splitext(filename)[1].lower()
        
        for category, exts in extensions.items():
            if file_ext in exts:
                category_path = os.path.join(target_path, category)
                
                # Naya folder banayein agar nahi hai toh
                os.makedirs(category_path, exist_ok=True)
                
                # File move karein
                shutil.move(filepath, os.path.join(category_path, filename))
                print(f"Moved: {filename} -> {category}")
                break

if __name__ == "__main__":
    # Yahan apna folder path dalein
    path = input("Enter the folder path to organize: ")
    organize_folder(path)
    print("Folder organized successfully!")
