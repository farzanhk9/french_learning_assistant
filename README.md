import random
import json
import os

FILENAME = "french_words.json"

# ---------------- Data Setup ----------------
def load_words():
    if os.path.exists(FILENAME):
        with open(FILENAME, "r", encoding="utf-8") as f:
            return json.load(f)
    # Default basic vocabulary
    words = [
        {"fr": "bonjour", "en": "hello"},
        {"fr": "merci", "en": "thank you"},
        {"fr": "amour", "en": "love"},
        {"fr": "chat", "en": "cat"},
        {"fr": "chien", "en": "dog"},
        {"fr": "maison", "en": "house"},
        {"fr": "livre", "en": "book"},
        {"fr": "fromage", "en": "cheese"},
        {"fr": "eau", "en": "water"},
        {"fr": "soleil", "en": "sun"},
    ]
    save_words(words)
    return words

def save_words(words):
    with open(FILENAME, "w", encoding="utf-8") as f:
        json.dump(words, f, indent=4, ensure_ascii=False)

# ---------------- Features ----------------
def add_word(words):
    print("\n➕ Add a new word")
    fr = input("🇫🇷 French word: ").strip().lower()
    en = input("🇬🇧 English meaning: ").strip().lower()
    words.append({"fr": fr, "en": en})
    save_words(words)
    print("✅ Word added successfully!")

def view_words(words):
    print("\n📘 Your French Vocabulary:")
    for i, w in enumerate(words, 1):
        print(f"{i}. {w['fr']} → {w['en']}")

def quiz(words):
    print("\n🎯 French Quiz — Let's test you!")
    random.shuffle(words)
    score = 0
    for w in words[:5]:
        answer = input(f"👉 What is '{w['fr']}' in English? ").strip().lower()
        if answer == w["en"]:
            print("✅ Correct!\n")
            score += 1
        else:
            print(f"❌ Wrong. The answer is '{w['en']}'.\n")
    print(f"🏁 Your score: {score}/5")

def main():
    words = load_words()
    while True:
        print("\n=== 🇫🇷 FRENCH LEARNING ASSISTANT ===")
        print("1️⃣ View words")
        print("2️⃣ Add new word")
        print("3️⃣ Take a quiz")
        print("4️⃣ Exit")

        choice = input("👉 Choose an option: ").strip()
        if choice == "1":
            view_words(words)
        elif choice == "2":
            add_word(words)
        elif choice == "3":
            quiz(words)
        elif choice == "4":
            print("👋 Au revoir! Keep learning French every day!")
            break
        else:
            print("⚠️ Invalid choice.")

if __name__ == "__main__":
    main()

