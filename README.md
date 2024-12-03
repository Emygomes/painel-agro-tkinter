# painel-agro-tkinter


import tkinter as tk
from tkinter import messagebox

def incrementar():
    global contador
    contador += 1
    atualizar_label()

def decrementar():
    global contador
    if contador > 0:
        contador -= 1
        atualizar_label()
    else:
        messagebox.showwarning("Aviso", "O valor já está em zero!")

def zerar():
    global contador
    contador = 0
    atualizar_label()

def salvar_historico():
    historico.append(contador)
    messagebox.showinfo("Histórico", f"Valor {contador} salvo!")
    atualizar_historico()

def atualizar_label():
    label_contador.config(text=f"{contador}")

def atualizar_historico():
    historico_texto = ", ".join(map(str, historico))
    historico_label.config(text=f"Histórico: {historico_texto}")

def exibir_historico():
    historico_texto = "\n".join(map(str, historico))
    messagebox.showinfo("Histórico Completo", f"Histórico Salvo:\n{historico_texto}")

# Configurações iniciais
contador = 0
historico = []

# Janela principal
janela = tk.Tk()
janela.title("Painel Agro Moderno")
janela.geometry("500x400")
janela.configure(bg="#f5f5f5")

# Estilo
estilo_titulo = {"font": ("Helvetica", 20, "bold"), "bg": "#f5f5f5", "fg": "#4CAF50"}
estilo_label = {"bg": "#f5f5f5", "fg": "#333"}
estilo_botao = {"font": ("Helvetica", 12), "bg": "#4CAF50", "fg": "white", "relief": "raised", "bd": 2}

# Título
titulo = tk.Label(janela, text="Painel de Contagem Agro", **estilo_titulo)
titulo.pack(pady=20)

# Contador central
label_contador = tk.Label(janela, text="0", font=("Helvetica", 40, "bold"), **estilo_label)
label_contador.pack(pady=20)

# Botões de ação
frame_botoes = tk.Frame(janela, bg="#f5f5f5")
frame_botoes.pack(pady=10)

btn_incrementar = tk.Button(frame_botoes, text="Adicionar", command=incrementar, **estilo_botao)
btn_incrementar.grid(row=0, column=0, padx=10)

btn_decrementar = tk.Button(frame_botoes, text="Remover", command=decrementar, **estilo_botao)
btn_decrementar.grid(row=0, column=1, padx=10)

btn_zerar = tk.Button(frame_botoes, text="Zerar", command=zerar, **estilo_botao)
btn_zerar.grid(row=0, column=2, padx=10)

# Botão para salvar no histórico
btn_salvar = tk.Button(janela, text="Salvar no Histórico", command=salvar_historico, **estilo_botao)
btn_salvar.pack(pady=20)

# Botão para exibir histórico completo
btn_ver_historico = tk.Button(janela, text="Ver Histórico Completo", command=exibir_historico, **estilo_botao)
btn_ver_historico.pack(pady=10)

# Exibição do histórico
historico_label = tk.Label(janela, text="Histórico: Nenhum valor ainda", **estilo_label)
historico_label.pack(pady=10)

# Rodapé
rodape = tk.Label(janela, text="Sistema de Gestão Agropecuária", font=("Helvetica", 10), bg="#f5f5f5", fg="#888")
rodape.pack(side="bottom", pady=10)

# Inicia o loop da interface
janela.mainloop()
