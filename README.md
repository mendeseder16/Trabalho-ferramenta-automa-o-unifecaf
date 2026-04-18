# Trabalho-ferramenta-automa-o-unifecaf

1. Parte Teórica: Análise do Caso
Contextualização do Desafio
Na transição para a Indústria 4.0 é essencial para manter a competitividade. A automação reduz o custo operacional e elimina a variabilidade humana no processo de conferência.

Estrutura do Raciocínio Lógico
A solução foi desenvolvida utilizando a linguagem Python, seguindo estas premissas:
•	Entrada de Dados: Recebe ID, peso, cor e comprimento de cada haste.
•	Decisões e Condições: O sistema aplica filtros lógicos para aprovação: Peso entre 95g e 105g; cores Azul ou Verde; comprimento entre 10cm e 20cm.
•	Gerenciamento de Armazenamento: Implementação de um contador que fecha caixas a cada 10 unidades aprovadas, garantindo a organização logística.

2. Parte Prática: Protótipo do Código
Abaixo, o código estruturado para atender a todos os requisitos do menu interativo.
Python
# Listas para armazenamento de dados
pecas_geral = []
caixas_fechadas = []
caixa_atual = []
total_reprovadas = 0
motivos_repro = {}

def cadastrar_peca():
    global total_reprovadas
    print("\n--- Cadastro de Nova Haste (Metal-Azul) ---")
    id_p = input("ID da Peça: ")
    peso = float(input("Peso (g): "))
    cor = input("Cor (azul/verde/outra): ").strip().lower()
    comp = float(input("Comprimento (cm): "))

    motivo = []
    if not (95 <= peso <= 105): motivo.append("Peso fora do padrão") [cite: 11]
    if cor not in ['azul', 'verde']: motivo.append("Cor não permitida") [cite: 13]
    if not (10 <= comp <= 20): motivo.append("Comprimento fora do padrão") [cite: 14]

    peca = {"id": id_p, "peso": peso, "cor": cor, "comp": comp}
    
    if not motivo:
        peca["status"] = "Aprovada"
        pecas_geral.append(peca)
        caixa_atual.append(peca)
        print(">>> Peça APROVADA e enviada para a linha de embalagem.")
        
        if len(caixa_atual) == 10: [cite: 15, 16]
            caixas_fechadas.append(list(caixa_atual))
            caixa_atual.clear()
            print("!!! CAIXA FECHADA (10 unidades) !!!")
    else:
        peca["status"] = "Reprovada"
        peca["motivo"] = ", ".join(motivo)
        pecas_geral.append(peca)
        total_reprovadas += 1
        print(f">>> Peça REPROVADA. Motivo: {peca['motivo']}")

def gerar_relatorio(): [cite: 17, 45]
    aprovadas = [p for p in pecas_geral if p["status"] == "Aprovada"]
    reprovadas = [p for p in pecas_geral if p["status"] == "Reprovada"]
    
    print("\n========== RELATÓRIO FINAL - METAL-AZUL ==========")
    print(f"Total de peças aprovadas: {len(aprovadas)}") [cite: 18]
    print(f"Total de peças reprovadas: {len(reprovadas)}") [cite: 20]
    print(f"Quantidade de caixas utilizadas: {len(caixas_fechadas)}") [cite: 22]
    
    if reprovadas:
        print("\nMotivos de Reprovação:")
        for r in reprovadas:
            print(f"- ID {r['id']}: {r['motivo']}") [cite: 20]
    print("================================================")

# O loop principal deve conter as opções do menu de 1 a 5 conforme solicitado 

3. Reflexão Final e Expansão
Benefícios Percebidos: A solução digital elimina o viés subjetivo da inspeção manual. O maior desafio no desenvolvimento foi a lógica de "limpeza" da lista caixa_atual para que novas peças não fossem somadas a caixas já fechadas.


