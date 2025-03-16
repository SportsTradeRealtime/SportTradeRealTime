import requests

class SportsTradingPlatform:
    def __init__(self, api_key):
        self.api_key = api_key
        self.base_url = "https://v3.football.api-sports.io"
        self.clubs = {
            "FC Barcelona": 150,
            "Real Madrid": 155,
            "Manchester United": 140,
            "Chelsea": 125,
            "Bayern Munich": 145,
        }
        self.balance = 1000  # Почетен биланс на корисникот
        self.transaction_fee = 0.02  # Провизија од 2%

    def fetch_real_prices(self):
        """Ажурирај цени за клубови преку API."""
        headers = {"x-rapidapi-key": self.api_key, "x-rapidapi-host": "v3.football.api-sports.io"}
        for club in self.clubs:
            try:
                response = requests.get(f"{self.base_url}/players/{club}", headers=headers)
                if response.status_code == 200:
                    data = response.json()
                    new_price = data.get("price", None)
                    if new_price:
                        self.clubs[club] = new_price
                        print(f"Ажурирана цена за {club}: ${new_price}")
                else:
                    print(f"Грешка при ажурирање на {club}: {response.status_code}")
            except Exception as e:
                print(f"Грешка при API повик: {e}")

    def show_club_prices(self):
        """Печати ги моменталните цени на клубовите."""
        print("\nМоментални Цени:")
        for club, price in self.clubs.items():
            print(f"{club}: ${price}")

    def buy_club(self, club, amount):
        """Купи акции за одреден клуб."""
        if club not in self.clubs:
            print(f"{club} не е достапен за тргување.")
            return
        price = self.clubs[club]
        total_cost = price * amount * (1 + self.transaction_fee)
        if total_cost > self.balance:
            print("Недоволно средства за оваа трансакција.")
        else:
            self.balance -= total_cost
            print(f"Купени {amount} акции од {club} за ${total_cost:.2f}. Нов биланс: ${self.balance:.2f}")

    def deposit(self, amount):
        """Депонирај средства."""
        if amount > 0:
            self.balance += amount
            print(f"Успешно депонирани ${amount}. Нов биланс: ${self.balance:.2f}")
        else:
            print("Износот за депозит мора да биде поголем од 0.")

    def withdraw(self, amount):
        """Повлечи средства."""
        if amount > self.balance:
            print("Недоволно средства за повлекување.")
        elif amount > 0:
            self.balance -= amount
            print(f"Успешно повлечени ${amount}. Нов биланс: ${self.balance:.2f}")
        else:
            print("Износот за повлекување мора да биде поголем од 0.")

def main():
    api_key = "630c9b3b32463a282338906e22db1fb8"
    platform = SportsTradingPlatform(api_key)

    while True:
        print("\n--- Sports Trading Platform ---")
        print("1. Прикажи Цени")
        print("2. Ажурирај Цени")
        print("3. Купи Акции")
        print("4. Депонирај Средства")
        print("5. Повлечи Средства")
        print("6. Излези")

        choice = input("Избери опција: ")
        if choice == "1":
            platform.show_club_prices()
        elif choice == "2":
            platform.fetch_real_prices()
        elif choice == "3":
            club = input("Внеси име на клуб: ")
            amount = int(input("Внеси број на акции: "))
            platform.buy_club(club, amount)
        elif choice == "4":
            amount = float(input("Внеси износ за депозит: "))
            platform.deposit(amount)
        elif choice == "5":
            amount = float(input("Внеси износ за повлекување: "))
            platform.withdraw(amount)
        elif choice == "6":
            print("Излез од платформата.")
            break
        else:
            print("Невалидна опција. Обиди се повторно.")

if __name__ == "__main__":
    main()
