    from time import sleep
    import random
    
    personagem = {
        "Rael": {
            "Classe": "Arqueiro",
            "HP": 150,
            "Ataque": {
                "Tiro de arco": 20,
                "Caixão de areia": 35,
                "Armadilha": {
                    "Preparo": 2,
                    "Dano": 80
                }
            }
        }
    }
    
    inimigo = {
        "Goblin": {
            "HP": 80,
            "Ataque": 15
        }
    }
    
    chefe_final = {
        "Baal": {
            "HP": 160,
            "Ataque": {
                "Soco": 30,
                "Vórtice": 50,
                "Sequência de socos": {
                    "Preparo": 3,
                    "Dano": 60
                }
            }
        }
    }
    
    nome_personagem = "Rael"
    dados_personagem = personagem[nome_personagem]
    preparo_armadilha = 0
    
    
    def escolher_ataque():
        while True:
            try:
                print("\nEscolha um ataque:")
                for i, (nome, valor) in enumerate(
                        dados_personagem["Ataque"].items(), start=1):
                    print(f"{i} - {nome}")
    
                escolha = int(input("> "))
    
                if 1 <= escolha <= len(dados_personagem["Ataque"]):
                    return escolha
    
                print("Ataque inválido!")
    
            except ValueError:
                print("Digite apenas números!")
    
    
    print("_" * 30)
    print("FICHA DE PERSONAGEM".center(30))
    print(nome_personagem.center(30))
    print("_" * 30)
    
    for atributo, valor in dados_personagem.items():
        if atributo != "Ataque":
            print(f"{atributo}: {valor}")
            sleep(0.5)
    
    print("\nATAQUES")
    print("_" * 30)
    
    for nome, valor in dados_personagem["Ataque"].items():
        if isinstance(valor, dict):
            print(f"{nome}:")
            for chave, dado in valor.items():
                print(f"  {chave}: {dado}")
        else:
            print(f"{nome}: {valor}")
    
        sleep(0.5)
    
    print("\nUm Goblin apareceu!")
    sleep(1)
    
    # ==========================
    # BATALHA CONTRA O GOBLIN
    # ==========================
    
    while inimigo["Goblin"]["HP"] > 0 and personagem["Rael"]["HP"] > 0:
    
        escolha = escolher_ataque()
    
        nome_ataque = list(dados_personagem["Ataque"].keys())[escolha - 1]
        ataque = dados_personagem["Ataque"][nome_ataque]
    
        print(f"\nRael usou {nome_ataque}!")
        sleep(1)
    
        if isinstance(ataque, dict):
    
            preparo_armadilha += 1
    
            print(f"Armadilha preparada ({preparo_armadilha}/{ataque['Preparo']})")
    
            if preparo_armadilha >= ataque["Preparo"]:
                dano = ataque["Dano"]
    
                print("\nA armadilha foi ativada!")
                sleep(1)
    
                inimigo["Goblin"]["HP"] -= dano
    
                print(f"Goblin sofreu {dano} de dano!")
                print(f"HP do Goblin: {max(0, inimigo['Goblin']['HP'])}")
    
                preparo_armadilha = 0
    
        else:
            inimigo["Goblin"]["HP"] -= ataque
    
            print(f"Rael causou {ataque} de dano!")
            print(f"HP do Goblin: {max(0, inimigo['Goblin']['HP'])}")
    
        if inimigo["Goblin"]["HP"] <= 0:
            print("\nGoblin derrotado!")
            break
    
        print("\nTurno do Goblin")
        sleep(1)
    
        dano_goblin = inimigo["Goblin"]["Ataque"]
    
        personagem["Rael"]["HP"] -= dano_goblin
    
        print(f"Goblin causou {dano_goblin} de dano!")
        print(f"HP de Rael: {max(0, personagem['Rael']['HP'])}")
    
        if personagem["Rael"]["HP"] <= 0:
            print("\nRael foi derrotado!")
            exit()
    
        sleep(1)
    
    # ==========================
    # CHEFE FINAL
    # =========================
    
    print("\nO poderoso Baal apareceu!")
    sleep(2)
    
    preparo_baal = 0
    
    while chefe_final["Baal"]["HP"] > 0 and personagem["Rael"]["HP"] > 0:
    
        escolha = escolher_ataque()
    
        nome_ataque = list(dados_personagem["Ataque"].keys())[escolha - 1]
        ataque = dados_personagem["Ataque"][nome_ataque]
    
        print(f"\nRael usou {nome_ataque}!")
        sleep(1)
    
        if isinstance(ataque, dict):
    
            preparo_armadilha += 1
    
            print(
                f"Armadilha preparada ({preparo_armadilha}/{ataque['Preparo']})")
    
            if preparo_armadilha >= ataque["Preparo"]:
    
                dano = ataque["Dano"]
    
                print("\nA armadilha foi ativada!")
                sleep(1)
    
                chefe_final["Baal"]["HP"] -= dano
    
                print(f"Baal sofreu {dano} de dano!")
                print(f"HP do Baal: {max(0, chefe_final['Baal']['HP'])}")
    
                preparo_armadilha = 0
    
        else:
    
            chefe_final["Baal"]["HP"] -= ataque
    
            print(f"Rael causou {ataque} de dano!")
            print(f"HP do Baal: {max(0, chefe_final['Baal']['HP'])}")
    
        if chefe_final["Baal"]["HP"] <= 0:
            print("\nBaal foi derrotado!")
            print("Você venceu o jogo!")
            break
    
        print("\nTurno do Baal")
        sleep(1)
    
        ataques_baal = chefe_final["Baal"]["Ataque"]
    
        nome_ataque_baal = random.choice(list(ataques_baal.keys()))
        ataque_baal = ataques_baal[nome_ataque_baal]
    
        if isinstance(ataque_baal, dict):
    
            preparo_baal += 1
    
            print(
                f"Baal está preparando {nome_ataque_baal} "
                f"({preparo_baal}/{ataque_baal['Preparo']})"
            )
    
            if preparo_baal >= ataque_baal["Preparo"]:
    
                dano = ataque_baal["Dano"]
    
                print(f"\nBaal usou {nome_ataque_baal}!")
                sleep(1)
    
                personagem["Rael"]["HP"] -= dano
    
                print(f"Rael sofreu {dano} de dano!")
                print(f"HP de Rael: {max(0, personagem['Rael']['HP'])}")
    
                preparo_baal = 0
    
        else:
    
            personagem["Rael"]["HP"] -= ataque_baal
    
            print(f"Baal usou {nome_ataque_baal}!")
            print(f"Rael sofreu {ataque_baal} de dano!")
            print(f"HP de Rael: {max(0, personagem['Rael']['HP'])}")
    
        if personagem["Rael"]["HP"] <= 0:
            print("\nRael foi derrotado!")
            break
    
        sleep(1)
