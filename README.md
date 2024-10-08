# QUIZ
import tkinter as tk
from tkinter import messagebox

perguntas = [
    "Qual é o jogo onde você deve sobreviver em uma ilha deserta?",
    "Qual é o famoso encanador da Nintendo?",
    "Em que jogo você explora o mundo de Hyrule?",
    "Qual jogo apresenta o personagem Master Chief?",
    "Qual é o famoso jogo de batalha real da Epic Games?",
    "Qual é o jogo onde você pilota carros em uma corrida de rua?",
    "Qual é o jogo onde você constrói e explora mundos feitos de blocos?",
    "Qual é o jogo de simulação de vida onde você cuida de uma aldeia?",
    "Em qual jogo você deve capturar criaturas chamadas 'Pokémon'?",
    "Qual é o jogo onde você é um assassino em um mundo histórico?"
]

respostas = [
    ["Stranded Deep", "The Forest", "Survivor", "Minecraft"],
    ["Mario", "Luigi", "Wario", "Yoshi"],
    ["The Legend of Zelda", "Final Fantasy", "Halo", "Dark Souls"],
    ["Halo", "Call of Duty", "Gears of War", "Fortnite"],
    ["Fortnite", "PUBG", "Apex Legends", "Battlefield"],
    ["Need for Speed", "Gran Turismo", "Forza", "Burnout"],
    ["Minecraft", "Terraria", "Roblox", "Fortnite"],
    ["Animal Crossing", "The Sims", "SimCity", "Harvest Moon"],
    ["Pokémon", "Digimon", "Monster Hunter", "Final Fantasy"],
    ["Assassin's Creed", "Hitman", "Watch Dogs", "Far Cry"]
]

respostas_corretas = [
    "Stranded Deep", "Mario", "The Legend of Zelda", "Halo", 
    "Fortnite", "Need for Speed", "Minecraft", "Animal Crossing", 
    "Pokémon", "Assassin's Creed"
]

class QuizApp:
    def __init__(self, master):
        self.master = master
        self.index_pergunta = 0

        self.label_pergunta = tk.Label(master, text="")
        self.label_pergunta.pack(pady=20)

        self.variavel_resposta = tk.StringVar()
        self.botoes_radio = []

        for i in range(4):
            botoes_radio = tk.Radiobutton(master, variable=self.variavel_resposta, value="", indicatoron=0)
            botoes_radio.pack(fill='x', padx=20, pady=5)
            self.botoes_radio.append(botoes_radio)

        self.botao_verificar = tk.Button(master, text="Verificar Resposta", command=self.verificar_resposta)
        self.botao_verificar.pack(pady=20)

        self.exibir_pergunta(self.index_pergunta)

    def verificar_resposta(self):
        if self.variavel_resposta.get() == respostas_corretas[self.index_pergunta]:
            messagebox.showinfo("Resultado", "Correto!")
        else:
            messagebox.showinfo("Resultado", f"Incorreto! A resposta certa é: {respostas_corretas[self.index_pergunta]}")

        if self.index_pergunta < len(perguntas) - 1:
            self.index_pergunta += 1
            self.exibir_pergunta(self.index_pergunta)
        else:
            messagebox.showinfo("Fim do Quiz", "Você completou o quiz!")

    def exibir_pergunta(self, index):
        self.label_pergunta.config(text=perguntas[index])
        self.variavel_resposta.set(None)  # Limpa a seleção
        for i, resposta in enumerate(respostas[index]):
            self.botoes_radio[i].config(text=resposta, value=resposta)

root = tk.Tk()
root.title("Quiz de Jogos Famosos")
app = QuizApp(root)
root.mainloop()
