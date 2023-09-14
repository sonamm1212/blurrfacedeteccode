# blurrfacedeteccode
real  time face detection of blurr face 
The code you provided is almost correct, but it has one small issue. The '13' you used in if cv2.waitKey(1) == 13: corresponds to the ENTER key, but it's more common to use the 'q' key to exit the loop. Here's the modified code with 'q' as the exit key:

python
Copy code
import cv2

# Load the pre-trained face detection Haar Cascade classifier
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + "haarcascade_frontalface_default.xml")

# Open the webcam
cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()

    if not ret:
        break

    # Convert frame to grayscale for face detection
    gray_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # Detect faces in the frame
    faces = face_cascade.detectMultiScale(gray_frame, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))

    for (x, y, w, h) in faces:
        # Extract the region of interest (ROI) for the face
        face_roi = frame[y:y+h, x:x+w]

        # Apply Gaussian blur to the face ROI
        blurred_face = cv2.GaussianBlur(face_roi, (99, 99), 20)

        # Place the blurred face back into the original frame
        frame[y:y+h, x:x+w] = blurred_face

    # Display the result
    cv2.imshow('Blurred Faces', frame)

    # Exit the loop when the 'q' key is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Release the video capture and close the window
cv2.destroyAllWindows()
cap.release()
This modified code will terminate the program when you press the 'q' key, which is more commonly used for this purpose.
