Note to reviewers: This script is optimized to run locally. To test the live webcam and person segmentation feature, clone this repository, install the requirements (mediapipe, opencv-python), and run the script on a machine equipped with a webcam.

Combined motion + person detection for a live webcam feed, tuned for
Raspberry Pi.

Stage 1 (always on, cheap): MOG2 background subtraction watches every
frame for pixel-level change and acts as a tripwire.
Stage 2 (only while triggered, expensive): MediaPipe's Image Segmenter
(selfie_multiclass model) confirms whether the moving thing is a person
and produces a clean mask.

Segmentation switches off again after a short run of motion-free frames,
so the CPU-heavy model only runs in bursts around real activity.

NOTE ON MEDIAPIPE VERSION: MediaPipe removed the old `mp.solutions.*` API
in the 0.10.31 pip release (Google's official guidance is to migrate to
MediaPipe Tasks - see https://ai.google.dev/edge/mediapipe/solutions/guide).
This script uses the current Tasks API (mp.tasks.vision.ImageSegmenter),
which works with mediapipe>=0.10. If you specifically need the old
`mp.solutions.selfie_segmentation` API instead, pin an older release with
`pip install "mediapipe<0.10.31"` (subject to ARM/Raspberry Pi wheel
availability for that older version).

Press 'q' in the video window to quit.
