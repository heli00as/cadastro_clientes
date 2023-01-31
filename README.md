# cadastro_clientes
rascunho de cadastro
import mysql.connector

conexao = mysql.connector.connect(
    host='localhost',
    user='root',
    password='K0kinhu$',
    database= 'tabelavendas',
)
operacao = 0
while operacao != 5:
    cursor = conexao.cursor()
    operacao = int(input('''Escolha a operação que deseja realizar:
[ 1 ] Inserir cliente
[ 2 ] Mostrar clientes cadastrados
[ 3 ] Alterar dados de cliente
[ 4 ] Deletar cadastro de cliente
[ 5 ] Sair do programa 
Opção:  '''))
#Parte 1
    if operacao == 1:
        nome = str(input('Nome comleto: ').title().strip())
        cpf = int(input('CPF: ').strip())
        cidade = str(input('Cidade: ').title().strip())
        email = str(input('E-mail: ').lower().strip())
        while '@' not in email:
            email = str(input('E-mail inválido: Digite novamente: '))
        comando = f'INSERT INTO tabela (cliente, cpf, cidade, email) VALUES ("{nome}", {cpf}, "{cidade}", "{email}")'
        cursor.execute(comando)
        conexao.commit()
        cursor.close()
        operacao = int(input('''Deseja continuar?
        [ 1 ] Sim
        [ 2 ] Não
        Operação:  '''))
        while not operacao <= 2 and operacao != 0:
            print('Comando inválido!')
            operacao = int(input('''Deseja continuar?
            [ 1 ] Sim
            [ 2 ] Não
            Operação:  '''))
        if operacao == 1:
                operacao = 0
        elif operacao == 2:
                operacao = 5
#Parte 2
    elif operacao == 2:
        comando ='SELECT * FROM tabela'
        cursor.execute(comando)
        retorno = cursor.fetchall()
        print(retorno)
        cursor.close()
        operacao = int(input('''Deseja continuar?
        [ 1 ] Sim
        [ 2 ] Não
        Operação:  '''))
        while not operacao <= 2 and operacao != 0:
            print('Comando inválido!')
            operacao = int(input('''Deseja continuar?
            [ 1 ] Sim
            [ 2 ] Não
            Operação:  '''))
        if operacao == 1:
                operacao = 0
        elif operacao == 2:
                operacao = 5
#Parte 3
    elif operacao == 3:
        opção = int(input('''Qual coluna deseja alterar?
[ 1 ] Nome
[ 2 ] CPF
[ 3 ] Cidade
[ 4 ] Email
Opção: '''))
        if opção == 1:
            dado = str(input('Digite exatamente o nome para alterar: '))
            nova = str(input('Alteração no nome: '))
            comando = f'UPDATE tabela SET "{nova}" WHERE cliente = "{dado}"'
        elif opção == 2:
            dado = int(input('Digite o CPF para alterar: '))
            nova = int(input('Alteração no CPF: '))
            comando = f'UPDATE tabela SET {nova} WHERE cpf = {dado}'
        elif opção == 3:
            dado = str(input('Digite a cidade atual para alterar: '))
            nova = str(input('Alteração no nome da Cidade: '))
            comando = f'UPDATE tabela SET "{nova}" WHERE cidade = "{dado}"'
        elif opção == 4:
            dado = str(input('Digite o E-mail atual para alterar: '))
            nova = str(input('Alteração no endereço de E-mail: '))
            comando = f'UPDATE tabela SET "{nova}" WHERE email = "{dado}"'
        else:
            operacao = int(input('''Deseja continuar?
        [ 1 ] Sim
        [ 2 ] Não
        Operação:  '''))
        while not operacao <= 2 and operacao != 0:
            print('Comando inválido!')
            operacao = int(input('''Deseja continuar?
            [ 1 ] Sim
            [ 2 ] Não
            Operação:  '''))
        if operacao == 1:
                operacao = 0
        elif operacao == 2:
                operacao = 5
#Parte 4
    elif operacao == 4:
        idTabela = int(input('Qual linha deseja excluir o cadastro?: '))
        comando = f'DELETE FROM tabela WHERE id = {idTabela}'
        cursor.execute(comando)
        conexao.commit()
        cursor.close()
        conexao.close()
        operacao = int(input('''Deseja continuar?
        [ 1 ] Sim
        [ 2 ] Não
        Operação:  '''))
        while not operacao <= 2 and operacao != 0:
            print('Comando inválido!')
            operacao = int(input('''Deseja continuar?
            [ 1 ] Sim
            [ 2 ] Não
            Operação:  '''))
        if operacao == 1:
                operacao = 0
        elif operacao == 2:
                operacao = 5
print('=+='*15)
print('Programa encerrado')
print('=+='*15)
