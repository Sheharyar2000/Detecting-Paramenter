# Detecting-Paramenter
Python code using OpenCV library to measure some basic parameters of a user's face using the camera

import cv2

# initialize the camera
cap = cv2.VideoCapture(0)

# initialize the face detection classifier
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + "haarcascade_frontalface_default.xml")

while True:
    # read a frame from the camera
    ret, frame = cap.read()

    # convert the frame to grayscale
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # detect faces in the frame
    faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))

    # loop over the detected faces and draw a rectangle around each face
    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 0), 2)

        # measure the distance between the eyes and the width of the face
        eye_distance = abs((x + w/2) - (x + w*0.3))
        face_width = w

        # print the measured parameters
        print("Eye distance:", eye_distance)
        print("Face width:", face_width)

    # display the resulting frame
    cv2.imshow('frame', frame)

    # exit the loop if the 'q' key is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# release the camera and close the window
cap.release()
cv2.destroyAllWindows()
