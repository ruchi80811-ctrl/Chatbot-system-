"""
TASK 1: Rule-Based Chatbot
CODSOFT AI Internship

A simple chatbot that uses pattern matching (regex) and predefined rules
to respond to user queries. Demonstrates basic NLP concepts like
keyword matching and conversation flow handling.
"""

import re
import random
from datetime import datetime


class RuleBasedChatbot:
    def __init__(self, name="CodBot"):
        self.name = name
        self.user_name = None

        # Each rule = (regex pattern, list of possible responses)
        self.rules = [
            (r'\b(hi|hello|hey|hii+)\b',
                ["Hello! How can I help you today?",
                 "Hey there! What can I do for you?",
                 "Hi! Nice to see you."]),

            (r'\bmy name is (\w+)',
                ["Nice to meet you, {0}!"]),

            (r'\b(how are you|how are u)\b',
                ["I'm just a program, but I'm running great! How about you?",
                 "Doing well, thanks for asking!"]),

            (r'\b(your name|who are you)\b',
                [f"I'm {self.name}, your friendly rule-based chatbot."]),

            (r'\b(time)\b',
                ["Let me check that for you..."]),  # handled specially below

            (r'\b(date|today)\b',
                ["Let me check that for you..."]),  # handled specially below

            (r'\b(bye|goodbye|exit|quit)\b',
                ["Goodbye! Have a great day!",
                 "See you later!",
                 "Bye! Take care."]),

            (r'\b(thank you|thanks)\b',
                ["You're welcome!",
                 "Anytime!",
                 "Glad I could help."]),

            (r'\b(help|what can you do)\b',
                ["I can chat with you, tell you the time/date, "
                 "and respond to greetings. Try saying 'hi' or 'what time is it'."]),

            (r'\b(joke)\b',
                ["Why do programmers prefer dark mode? Because light attracts bugs!",
                 "I told my computer I needed a break, and it said 'No problem, I'll go to sleep.'"]),
        ]

    def get_response(self, user_input):
        text = user_input.lower().strip()

        # Special handling for time/date (dynamic content)
        if re.search(r'\btime\b', text):
            return f"The current time is {datetime.now().strftime('%H:%M:%S')}."
        if re.search(r'\b(date|today)\b', text):
            return f"Today's date is {datetime.now().strftime('%Y-%m-%d')}."

        for pattern, responses in self.rules:
            match = re.search(pattern, text)
            if match:
                response = random.choice(responses)
                if match.groups():
                    self.user_name = match.group(1).capitalize()
                    return response.format(self.user_name)
                return response

        # Fallback if no rule matches
        fallback = [
            "I'm not sure I understand. Could you rephrase that?",
            "Hmm, I don't have a rule for that yet. Try asking something else.",
            "Sorry, I didn't get that. Type 'help' to see what I can do."
        ]
        return random.choice(fallback)

    def chat(self):
        print(f"{self.name}: Hello! I'm {self.name}. Type 'bye' to exit.\n")
        while True:
            user_input = input("You: ")
            if not user_input.strip():
                continue
            response = self.get_response(user_input)
            print(f"{self.name}: {response}")
            if re.search(r'\b(bye|goodbye|exit|quit)\b', user_input.lower()):
                break


if __name__ == "__main__":
    bot = RuleBasedChatbot()
    bot.chat()
