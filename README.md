# Final-Project-Emotion-Detector
Final Project: Emotion Detector

TASK 1 
git clone <forked_repository_url>
cd <repository_name>

python -m venv env
.\env\Scripts\activate

pip install -r requirements.txt

TASK 2 
Create an Emotion Detection Application Using Watson NLP Library
pip install ibm-watson

Integrate Watson NLP:
from ibm_watson import NaturalLanguageUnderstandingV1
from ibm_watson.natural_language_understanding_v1 import Features, EmotionOptions
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

def analyze_emotion(text):
    # Replace with your API key and URL
    authenticator = IAMAuthenticator('your_api_key')
    nlu = NaturalLanguageUnderstandingV1(
        version='2024-01-01',
        authenticator=authenticator
    )
    nlu.set_service_url('your_service_url')

    response = nlu.analyze(
        text=text,
        features=Features(emotion=EmotionOptions())
    ).get_result()

    return response['emotion']['document']['emotion']

    TEST 
    if __name__ == "__main__":
    sample_text = "I am thrilled about the new product!"
    emotions = analyze_emotion(sample_text)
    print("Emotions detected:", emotions)

    FORMAT
    def format_emotions(emotions):
    formatted = "\n".join(
        [f"{emotion.capitalize()}: {score:.2f}" for emotion, score in emotions.items()]
    )
    return f"Detected Emotions:\n{formatted}

    UPDATE
    if __name__ == "__main__":
    sample_text = "I am thrilled about the new product!"
    emotions = analyze_emotion(sample_text)
    print(format_emotions(emotions))

    PACKAGE
    project/
├── app.py
├── requirements.txt
├── setup.py
├── tests/
│   └── test_app.py
├── static/
└── templates/

CREATE setup.py FILE
from setuptools import setup, find_packages

setup(
    name='emotion_detection',
    version='1.0.0',
    packages=find_packages(),
    install_requires=[
        'ibm-watson',
        'Flask',
    ],
)

GENERATE 
pip freeze > requirements.txt

RUN UNIT TESTS
Add tests in tests/test_app.py
import unittest
from app import analyze_emotion

class TestEmotionDetection(unittest.TestCase):
    def test_positive_emotion(self):
        text = "I am so happy with this service!"
        emotions = analyze_emotion(text)
        self.assertGreater(emotions.get('joy', 0), 0)

if __name__ == "__main__":
    unittest.main()

    RUN TESTS:
    python -m unittest discover -s tests

    DEPLOY AS WEB USING FLASK 
    from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def home():
    if request.method == "POST":
        text = request.form.get("text", "")
        emotions = analyze_emotion(text)
        return jsonify(emotions)
    return '''
        <form method="post">
            <textarea name="text"></textarea>
            <button type="submit">Analyze Emotion</button>
        </form>
    '''

if __name__ == "__main__":
    app.run(debug=True)

    RUN FLASK 
    flask run

    ERROR HANDLINGdef analyze_emotion(text):
    try:
        # Watson analysis logic
        ...
    except Exception as e:
        return {"error": str(e)}

        ADD ERROR HANDLING TO FLASK
        @app.errorhandler(500)
def handle_error(e):
    return jsonify({"error": "Internal Server Error"}), 500

    INSTALL PLYLINT
    pip install pylint

    ANALYZE 
    pylint app.py

    END.
    
    
    

