# jogo-adivinhacao-python

    import random

    print("🎯 Jogo da Adivinhação 🎯")
    print("Você tem 5 tentativas, boa sorte!!!")


    def erros(dificuldade, valor):
        if dificuldade == 1:
            if 1 > valor or valor > 20:
                print("❗ O número deve ser entre 1 e 20")
                return False
        elif dificuldade == 2:
            if 1 > valor or valor > 30:
                print("❗ O número deve ser entre 1 e 30")
                return False
        elif dificuldade == 3:
            if 1 > valor or valor > 40:
                print("❗ O número deve ser entre 1 e 40")
                return False
        elif dificuldade == 4:
            if 1 > valor or valor > 50:
                print("❗ O número deve ser entre 1 e 50")
                return False
        return True


    while True:
        try:
            dificuldade = int(input(
                "\n 1. Fácil [Números de 1 a 20]"
                "\n 2. Média [Números de 1 a 30]"
                "\n 3. Difícil [Números de 1 a 40]"
                "\n 4. Impossível [Números de 1 a 50]"
                "\n Escolha a dificuldade: "
        ))
    except ValueError:
        print("Digite um número inteiro.")
        continue

    if dificuldade > 4 or dificuldade < 1:
        print("Por favor, digite um número válido.")
        continue

    limites = {1: 20, 2: 30, 3: 40, 4: 50}
    limite = limites.get(dificuldade, 20)
    numero = random.randint(1, limite)
    tentativas = 0

    try:
        chose = int(input(f"Escolha um valor entre 1 e {limite}: "))
    except ValueError:
        print("O número deve ser inteiro.")
        continue

    if not erros(dificuldade, chose):
        continue

    if numero < chose:
        print("O número correto é menor.")
    elif numero > chose:
        print("O número correto é maior.")

    tentativas += 1

    if chose != numero:
        esc = False
        while not esc:
            try:
                novo = int(input("Escolha um novo número: "))
            except ValueError:
                print("Escreva um número inteiro.")
                continue

            if not erros(dificuldade, novo):
                continue

            tentativas += 1

            if tentativas >= 5 and novo != numero:
                print(f"Você perdeu. O número era {numero} \nTentativas: 5")
                break

            if numero < novo:
                print("O número correto é menor.")
            elif numero > novo:
                print("O número correto é maior.")
            elif numero == novo:
                print(f"Você acertou!!! O número era: {numero}")
                print(f"Tentativas: {tentativas}")
                esc = True
    else:
        print(f"Você acertou de primeira!!! O número era: {numero}")
        print("Tentativas: 1")

    again = input("Você gostaria de jogar de novo? [y / n]: ").lower().strip()

    if again == "y":
        print("\n🔁 Novo jogo iniciado!\n")
        continue
    elif again == "n":
        print("\n👋 Obrigado por jogar! Até a próxima!")
        break
    else:
        print("\n❗ Escolha inválida. Encerrando o jogo.")
        break
