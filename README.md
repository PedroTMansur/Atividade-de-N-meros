# Atividade-de-N-meros

!pip install matplotlib

import random

import matplotlib.pyplot as plt

class GameAgent:
    def __init__(self, secret_number, max_attempts=5):
        self.secret_number = secret_number
        self.max_attempts = max_attempts
        self.attempts = 0
        self.state = "Esperando tentativa"
        self.history = []  # Histórico de tentativas

    def make_guess(self, guess):
        self.attempts += 1
        self.history.append(guess)

        if guess == self.secret_number:
            self.state = "Acertou!"
            return "Parabéns! Você acertou o número."
        elif self.attempts >= self.max_attempts:
            self.state = "Fim do jogo"
            return f"Game Over! O número era {self.secret_number}."
        elif guess < self.secret_number:
            self.state = "Tentativa errada (muito baixo)"
            return "O número é maior. Tente novamente."
        else:
            self.state = "Tentativa errada (muito alto)"
            return "O número é menor. Tente novamente."
            import matplotlib.pyplot as plt

def plot_attempts(agent):
    plt.figure(figsize=(8,5))
    plt.plot(range(1, len(agent.history) + 1), agent.history, marker='o', linestyle='-')
    plt.axhline(y=agent.secret_number, color='r', linestyle='--', label='Número Secreto')
    plt.xlabel("Tentativas")
    plt.ylabel("Valor do Palpite")
    plt.title("Evolução das Tentativas do Jogador")
    plt.legend()
    plt.show()

    import random
import matplotlib.pyplot as plt

def selecionar_dificuldade():
    dificuldades = {
        "1": ("Fácil", 10, None, False, False),
        "2": ("Médio - Apenas Pares", 50, None, False, True),
        "3": ("Difícil - Apenas Primos", 100, 7, True, False)
    }

    print("Selecione a dificuldade:")
    for chave, valor in dificuldades.items():
        print(f"{chave} - {valor[0]}")

    escolha = input("Digite o número da dificuldade desejada: ")

    while escolha not in dificuldades:
        print("Opção inválida! Tente novamente.")
        escolha = input("Digite o número da dificuldade desejada: ")

    print(f"Você escolheu: {dificuldades[escolha][0]}")
    return dificuldades[escolha]

def gerar_numero_secreto(range_max, apenas_impares_e_primos, apenas_pares):
    def is_prime(n):
        if n < 2:
            return False
        for i in range(2, int(n ** 0.5) + 1):
            if n % i == 0:
                return False
        return True

    if apenas_impares_e_primos:
        numeros_validos = [n for n in range(1, range_max + 1) if is_prime(n)]
        return random.choice(numeros_validos)

    if apenas_pares:
        numeros_validos = [n for n in range(2, range_max + 1, 2)]
        return random.choice(numeros_validos)

    return random.randint(1, range_max)

class GameAgent:
    def __init__(self, secret_number, max_attempts=None):
        self.secret_number = secret_number
        self.attempts = 0
        self.max_attempts = max_attempts
        self.state = "Jogando"
        self.guess_history = []

    def make_guess(self, guess):
        self.attempts += 1
        self.guess_history.append(guess)
        if guess == self.secret_number:
            self.state = "Acertou!"
            return f"Parabéns! Você acertou em {self.attempts} tentativas."
        elif self.max_attempts and self.attempts >= self.max_attempts:
            self.state = "Fim do jogo"
            return f"Fim do jogo! O número secreto era {self.secret_number}."
        elif guess < self.secret_number:
            return "Tente um número maior."
        else:
            return "Tente um número menor."

def plot_attempts(agent):
    plt.plot(range(1, len(agent.guess_history) + 1), agent.guess_history, marker='o', linestyle='-')
    plt.axhline(y=agent.secret_number, color='r', linestyle='--', label='Número Secreto')
    plt.xlabel("Tentativas")
    plt.ylabel("Palpites")
    plt.title("Histórico de Tentativas")
    plt.legend()
    plt.show()

dificuldade, range_max, max_attempts, apenas_impares_e_primos, apenas_pares = selecionar_dificuldade()

agent = GameAgent(secret_number=gerar_numero_secreto(range_max, apenas_impares_e_primos, apenas_pares), max_attempts=max_attempts)

while agent.state not in ["Acertou!", "Fim do jogo"]:
    try:
        guess = int(input(f"Digite um número entre 1 e {range_max}: "))
        print(agent.make_guess(guess))
    except ValueError:
        print("Por favor, digite um número válido.")
plot_attempts(agent)
