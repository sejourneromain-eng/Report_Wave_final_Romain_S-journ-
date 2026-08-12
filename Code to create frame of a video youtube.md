# Report_Wave_final_Romain_S-journ-
# Code to create frame of a video youtube

# 1. INSTALL DEPENDENCIES AND DRIVE LINK


!pip install yt-dlp -q


import cv2
import os
from google.colab import drive


# 2. PATH CONFIGURATION ON THE DRIVE


# The link to the YouTube wave video
URL_YOUTUBE = "https://www.youtube.com/watch?v=_peYurDAq5Y"


# Main project folder on the Drive
# (The script will automatically create folders if they don't exist)
DRIVE_PROJECT_FOLDER = "/content/drive/MyDrive/Project_Yolo_v9"


# Full path where the video will be stored temporarily in your Drive
DRIVE_VIDEO_PATH = os.path.join(DRIVE_PROJECT_FOLDER, "Wave_vidéo", "video_youtube_vagues.mp4")


# Exact folder on your Drive where the images will be saved
DESTINATION_IMAGES_FOLDER = os.path.join(DRIVE_PROJECT_FOLDER, "Wave_Pictures", "dataset_youtube")


# EXTRACTION INTERVAL
FRAME_INTERVAL = 12




# 3. DOWNLOAD AND SPLITTING FUNCTIONS


def download_youtube(url, output_path):
    print(f"Downloading video from YouTube...")


    # Create the video subfolder if it doesn't exist in the Drive
    parent_folder = os.path.dirname(output_path)
    if not os.path.exists(parent_folder):
        os.makedirs(parent_folder)


    # Use yt-dlp to force a standard mp4 format directly into the Drive
    os.system(f'yt-dlp -f "bv*[ext=mp4]+ba[ext=m4a]/b[ext=mp4]" {url} -o "{output_path}"')


    if os.path.exists(output_path):
        print(f"-> Video successfully saved to your Drive: {output_path}")
    else:
        print("Error downloading the video.")


def split_video(video_path, output_folder, interval):
    if not os.path.exists(video_path):
        print(f"Error: Unable to split, video not found: {video_path}")
        return


    # Create the images subfolder if it doesn't exist in the Drive
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)
        print(f"Destination folder created in Drive: {output_folder}")


    cap = cv2.VideoCapture(video_path)
    total_frames = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))
    fps = int(cap.get(cv2.CAP_PROP_FPS))


    print(f"\nDetected video structure:")
    print(f"-> Total number of frames: {total_frames}")
    print(f"-> Number of FPS: {fps}")
    print(f"-> Scheduled splitting: 1 image every {interval} frames.\n")


    frame_idx = 0
    saved_images = 0


    while True:
        ret, frame = cap.read()
        if not ret:
            break  # End of video reached


        # Save the image to the Drive only if we hit the interval
        if frame_idx % interval == 0:
            image_name = f"yt_vague_frame_{frame_idx:06d}.jpg"
            image_path = os.path.join(output_folder, image_name)
            cv2.imwrite(image_path, frame)
            saved_images += 1


        frame_idx += 1


    cap.release()
    print(f"🚀 Done! {saved_images} images have been directly written and saved to your Google Drive.")




# 4. SCRIPT EXECUTION


# Step A: Direct download to the Drive
download_youtube(URL_YOUTUBE, DRIVE_VIDEO_PATH)


# Step B: Splitting and direct extraction to the Drive
split_video(DRIVE_VIDEO_PATH, DESTINATION_IMAGES_FOLDER, FRAME_INTERVAL)
