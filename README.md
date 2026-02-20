
||~~ Face Attendance System

Simple face-recognition-based attendance recorder using your webcam.

|~What it does
-- Detects faces from the webcam using `face_recognition` and OpenCV.
- -Matches detected faces against images in the `images/` folder (one subfolder per person).
-- Writes a line to `attendance.csv` the first time a person is seen each run: `Name,HH:MM:SS`.
-- Stores known face encodings in `encodings.pickle` after the first run for faster startup.

|~Prerequisites

- Python 3.8+(python-3.11.9)
- On Windows, installing `dlib` may require Visual Studio Build Tools and `cmake`.

Recommended install (try in an elevated or developer PowerShell):

``powershell
python -m pip install --upgrade pip
python -m pip install cmake
python -m pip install dlib
python -m pip install face_recognition opencv-python 
python -m pip install numpy==1.26.4


If you have trouble installing `dlib` via pip, install dlib-19.24.1 externally from github

|~Project structure

-- [attendance.py](attendance.py) — main script to run.

- images/ — one subfolder per person (folder name = person name). Place sample photos inside each person's folder.

- encodings.pickle — generated automatically on first run (contains face encodings).
- attendance.csv — attendance log (the repo includes a CSV; if missing create one with header `Name,Time`).

|~Current example image layout (already present):

images/
	Jeetu
    |-jeetu 1
    |-jeetu2
    |-...
    /
	Rimjhim/
	Sonu Soni/
	Sudhanshu/
	Sumit/


|~Prepare data

1. For each person, create a folder under `images/` named exactly how you want the name to appear in attendance (e.g., `images/John_Doe/`).
2. Put one or more clear face photos (front-facing) into that folder.

~Usage
1. Ensure `attendance.csv` exists. If not, create it and add a header line:

```csv
Name,Time
```

2. Run the script from the project root:

```powershell
python attendance.py
```

3. On first run the script will compute encodings (may take time) and save them to `encodings.pickle`. Subsequent runs will be faster.
4. When a known person is detected, their name is shown on the camera window and added to `attendance.csv` (only once per file run).
5. Press Enter in the camera window to exit.

|~Notes & troubleshooting

- If faces are not recognized, ensure your dataset images contain clearly visible frontal faces and good lighting.
- If `encodings.pickle` becomes stale or you update images, delete it to force recomputation on the next run.
- If `attendance.csv` is missing and you get an error opening it in `r+` mode, create the file beforehand (see header above) or change the script to open with append mode (`a+`).

|~Customization:

- To change camera resolution, edit the `cap.set(cv2.CAP_PROP_FRAME_WIDTH/HEIGHT, ...)` values in `attendance.py`.
- To use a different camera device, change `cv2.VideoCapture(0)` to the desired device index.

Simple face-recognition attendance script using `face_recognition` and OpenCV.
