# Projeto-de-sexta-


import numpy as np
import tkinter as tk
import time

# Inicializa o ambiente com sujeira em posições aleatórias
ambiente = np.random.choice([0, 1], size=(4, 4), p=[0.5, 0.5])


class AgenteAspirador:
    def __init__(self):
        self.energia = 100
        self.sacola = 0
        self.posicao = [0, 0]  # Agora o agente sempre começa no ponto [0, 0]
        self.estado = "desligado"

    def observar_ambiente(self):
        return ambiente[self.posicao[0], self.posicao[1]]

    def limpar_sujeira(self):
        if ambiente[self.posicao[0], self.posicao[1]] == 1:
            ambiente[self.posicao[0], self.posicao[1]] = 0
            self.sacola += 1
            self.energia -= 1

    def esvaziar_sacola(self):
        self.sacola = 0

    def determinar_acao(self):
        if self.estado == "desligado":
            return None

        sujeiras = []
        for i in range(4):
            for j in range(4):
                if ambiente[i, j] == 1:
                    sujeiras.append([i, j])

        if self.sacola == 10:
            self.retornar_casa()
            self.esvaziar_sacola()
