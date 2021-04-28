# Intrusion Detection 

The intrusion detection system demonstrates how to create a system that uses
google cloud fucntions and VGGFace to recognize the face. cloud Pub/Sub to send
notifications to a PWA app, in the case that someone enters the room that isn't
recognized by the VGGFace model. The user can then send a message via the PWA
app that would be seen by the intruder.

## Screenshots

[(Watch the demo on YouTube)][demo-yt]

## Schematics

![Schematics](schematics.jpg)

## Pre-requisites

- Breadboard
- Speaker
- Camera, any webcam would do
- Potentionmeter
- Google Cloud project with
  - TTS API enabled enabled
  - Google cloud fucntion where the face prediction is going to take place
  - Google Pub/Sub which is used to:
    - Send notification to PWA if an intruder is detected
    - Send message to rpi with the text to display
- Open weather API
- NPM packages
  - next
  - next-pwa
  - react
  - react-dom

## Setup and Build

To setup, follow these steps below.

1.  Create .env file in the keys folder 
2.  Obtain weather API.
    - Head to https://openweathermap.org/
    - Create an account
    - Get a free API key
    - add OPEN_WEATHER_MAP_API_KEY=*"api key obtained"* to the file
3.  Get your location
    - Head to https://www.latlong.net/
    - Type in your address
    - Add Longitude to .env file
      -LONGITUDE=*"your longitude"*
    - Add lattitude to .env file
      -LATTITUDE= *"your lattitude"*
4.  Get cloud tts credentials.json and add it to the key folder
    - Follow this tutorial for more details https://cloud.google.com/docs/authentication/getting-started
5.  Create cloud function
    - Go to https://console.cloud.google.com/functions and create a function
      -Be extra careful to make sure that function doesn't require authentication, otherwise the
      application wouldn't work straight out of the box
    - Change the language from node to python 3.7 <
    - Copy the contents of the feature/cloud_detection branch into the cloud function
    - Deploy the function, resolve any errors if needbe
    - Copy the link and add it to the ENV file
      -GOOGLE_FUNCTION_LINK="*your google function trigger link*"
6. To use the PWA locally
    - Make sure to give the project a valid ssl certificate 
    - Ensure that you have NPM setup proper
    - Pull from the feature/pwa branch to get the project
    - Run the command
      - npm install
      - npm run dev
To Be Added: Pub/Sub setup and GIO setup 

## Running

To run the main-module on the RPI:

  1. Ensure that you have python3.7 or higher
  2. Run the command
    - sudo python3 main
      - You should get an error with missing packages, working on a requirements.txt atm
    but for now install the libraries manually as python3 complains
    - pip3 install *missing libraries*
      - If pip3 doesn't exist, install it with the command: sudo apt install python3-pip
[demo-yt]: https://www.youtube.com/jamil-zaitouny
