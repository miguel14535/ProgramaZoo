# classe para os animais
class Animal:
    def __init__(self, nome, idade, barulho, movimento, alimentacao, habitat, horas_alimentacao):
        # Inicializa os atributos básicos do animal
        self.nome = nome
        self.idade = idade
        self.barulho = barulho
        self.movimento = movimento
        self.alimentacao = alimentacao
        self.habitat = habitat
        self.vizinhos = []  # armazenar os vizinhos dos animais
        self.horas_alimentacao = horas_alimentacao

    # Adiciona um vizinho à lista de vizinhos do animal
    def adicionar_vizinho(self, animal):
        if len(self.vizinhos) < 2:  # Permite no máximo 2 vizinhos
            self.vizinhos.append(animal.nome)

    # uma string com todas as informações do animal
    def exibir_info(self):
        return (f"Nome: {self.nome}\n"
                f"Idade: {self.idade}\n"
                f"Barulho: {self.barulho}\n"
                f"Movimento: {self.movimento}\n"
                f"Alimentação: {self.alimentacao}\n"
                f"Habitat: {self.habitat}\n"
                f"Vizinhos: {', '.join(self.vizinhos)}\n"
                f"Horário de Alimentação: {self.horas_alimentacao}")

    # alimentação dos animais
    def alimentar(self):
        return f"O {self.nome} foi alimentado."

# Define a classe Mamifero, que herda de Animal e adiciona a categoria "Mamífero"
class Mamifero(Animal):
    def __init__(self, nome, idade, barulho, movimento, alimentacao, habitat, horas_alimentacao):
        super().__init__(nome, idade, barulho, movimento, alimentacao, habitat, horas_alimentacao)
        self.categoria = "Mamífero"

# Define a classe Ave, que herda de Animal e adiciona a categoria "Ave"
class Ave(Animal):
    def __init__(self, nome, idade, barulho, movimento, alimentacao, habitat, horas_alimentacao):
        super().__init__(nome, idade, barulho, movimento, alimentacao, habitat, horas_alimentacao)
        self.categoria = "Ave"

# Define a classe Reptil, que herda de Animal e adiciona a categoria "Réptil"
class Reptil(Animal):
    def __init__(self, nome, idade, barulho, movimento, alimentacao, habitat, horas_alimentacao):
        super().__init__(nome, idade, barulho, movimento, alimentacao, habitat, horas_alimentacao)
        self.categoria = "Réptil"

# criar e cadastrar uma lista de animais
def cadastro_animais():
    animais = [
        Mamifero("tigre", 5, "Rugido", "Andar", "Carnívoro", "Selva", "11:00"),
        Ave("milhafre", 3, "Cricrí", "Voar", "Carnívoro", "Floresta", "10:00"),
        Reptil("iguana", 2, "Sibilo", "Rastejar", "Carnívoro", "Deserto", "9:00"),
        Mamifero("hipopótamo", 10, "Andar", "Grunhidos", "Herbívoro", "Savanas", "18:00"),
        Ave("falcão", 4, "klee-klee-klee", "Voar", "Carnívoro", "Floresta Tropical", "8:00"),
        Reptil("Tartaruga", 7, "Murmúrio", "Andar", "Herbívoro", "Praia", "12:00"),
    ]
    return animais

# exibir o menu de opções
def exibir_menu():
    print("\nMenu:")
    print("1. Mostrar todos os animais")
    print("2. Buscar animal")
    print("3. Mostrar animais por categoria")
    print("4. Listar vizinhos de um animal")
    print("5. Simular alimentação")
    print("6. Sair")

# listar todos os animais cadastrados
def listar_todos_animais(animais):
    print("\nLista de Animais:")
    for animal in animais:
        print(animal.nome)

# buscar um animal pelo nome e exibir suas informações
def buscar_animal(animais, nome):
    for animal in animais:
        if animal.nome.lower() == nome.lower():
            print(animal.exibir_info())
            return
    print("Animal não encontrado.")

# listar animais por categoria Mamífero, Ave ou Réptil
def listar_animais_por_categoria(animais, categoria):
    print(f"\nLista de Animais - Categoria: {categoria}:")
    for animal in animais:
        if animal.categoria == categoria:
            print(animal.nome)

# listar os vizinhos de um animal pelo nome
def listar_vizinhos(animais, nome):
    for animal in animais:
        if animal.nome.lower() == nome.lower():
            print(f"Vizinhos do {animal.nome}: {', '.join(animal.vizinhos)}")
            return
    print("Animal não encontrado.")

# simular a alimentação de um animal
def simular_alimentacao(animais, nome):
    for animal in animais:
        if animal.nome.lower() == nome.lower():
            print(animal.alimentar())
            return
    print("Animal não encontrado.")

def main():
    animais = cadastro_animais()
    
    # Adiciona vizinhos aos animais
    animais[0].adicionar_vizinho(animais[3])
    animais[0].adicionar_vizinho(animais[5])
    animais[1].adicionar_vizinho(animais[4])
    animais[2].adicionar_vizinho(animais[5])
    
    while True:
        exibir_menu()
        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            listar_todos_animais(animais)
        elif opcao == "2":
            nome = input("Digite o nome do animal: ")
            buscar_animal(animais, nome)
        elif opcao == "3":
            categoria = input("Digite a categoria (Mamífero, Ave, Réptil): ")
            listar_animais_por_categoria(animais, categoria)
        elif opcao == "4":
            nome = input("Digite o nome do animal: ")
            listar_vizinhos(animais, nome)
        elif opcao == "5":
            nome = input("Digite o nome do animal: ")
            simular_alimentacao(animais, nome)
        elif opcao == "6":
            print("Saindo...")
            break
        else:
            print("Opção inválida, tente novamente.")

# Ponto de entrada do programa
if __name__ == "__main__":
    main()
