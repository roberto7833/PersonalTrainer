# Sistema Personal Trainer
Somos alunos do curso de Ciência da Computação da Universidade Federal
da Paraiba (UFPB) Campus IV Rio Tinto. Fazemos parte de um projeto
da disciplina de Engenharia de Software, ministrada pelo Profº Dorgival
Netto, onde temos o objetivo de atender e analisar todos os requisitos de um
cliente real, utilizando as diversas práticas da Engenharia de Software.

# Compreensão do Sistema

1. Contexto:
Muitos profissionais que atuam como Personal Trainer gerenciam os treinos dos alunos
usando blocos de notas ou whatsapp. Isso pode gerar desorganização, perda do histórico
da evolução daquele aluno e muitas das vezes dificuldade por parte do profissional de
acompanhar se o treino está sendo feito da forma correta.

2. Objetivo do sistema:
Desenvolver um Sistema que auxilie o profissional a conduzir a gestão de treinos,
permitindo que o Personal monte a rotina dos alunos e os alunos acessem suas fichas de
forma digital e interativa, também permitir que o personal gerencie formas de pagamento, e
acompanhe os alunos que estão em dia com a mensalidade.
3. Quem vai usar?
Personal Trainer: Cadastrar os alunos, criar os treinos, cadastrar os exercícios, acompanhar
o progresso do aluno, gerenciar os pagamentos.
Aluno: Visualizar o Treino do dia, marcar os exercícios como concluído, registrar
feedback(como carga pesada, ou dificuldade para tal exercício), acompanhar informações
das mensalidades.

4. Requisitos Iniciais:

Para o personal:
Fazer Login.
Cadastrar aluno, Editar informações, Excluir aluno.
Criar treinos, acompanhar treinos, Editar treinos, excluir treino.
Visualizar histórico de evolução dos alunos.
acompanhar pagamentos das mensalidades.

para o Aluno:
Fazer Login.
Visualizar o treino do dia.
marcar treino como concluído
acompanhar progresso.
visualizar Histórico das mensalidades.
Solicitar acompanhamento ou tirar dúvidas com o professor.
deixar Feedback dos treinos.

# Padrões de Projeto (Design Patterns) - Sistema Personal Trainer

---

## 1. Padrões Criacionais

### Factory Method (para criação de perfis de usuário)
* **Aplicação:** As classes `Aluno`, `Personal` e `Administrador` utilizam herança da classe `Usuario`.
* **Propósito:** Encapsular a lógica de criação de cada perfil de usuário no sistema, permitindo instanciar o tipo correto com base nas permissões ou no parâmetro `TipoDoPerfil` (`ADM`, `PERSONAL`, `ALUNO`).

### Builder (para montagem de TreinoAluno)
* **Aplicação:** Na construção da rotina de treino do aluno (`TreinoAluno`), que é composta por uma coleção de objetos `ItemExercicio` e associada a um `Exercicio`.
* **Propósito:** Facilitar a criação gradual e configurável de uma ficha de treino, definindo divisões, repetições, séries, carga atual e tempo de descanso sem sobrecarregar construtores.

---

## 2. Padrões Estruturais

### Composite (para Estrutura do Treino)
* **Aplicação:** Associação entre `TreinoAluno`, `ItemExercicio` e `Exercicio`.
* **Propósito:** Tratar treinos compostos e exercícios individuais de maneira unificada, permitindo que um treino seja composto por agrupamentos de exercícios (como superséries) de forma hierárquica.

### Facade (para Serviços do Sistema)
* **Aplicação:** Criação de uma camada de serviço (ex.: `TreinoFacade` ou `UsuarioFacade`) para intermediar a comunicação entre as visões (`View`) e as classes de modelo (`Usuario`, `TreinoAluno`, `Conta`).
* **Propósito:** Oferecer uma interface simplificada para as operações do sistema (como cadastrar aluno, prescrever treino e registrar feedback), reduzindo o acoplamento direto com as entidades.

---

## 3. Padrões Comportamentais

### State (para Gerenciamento de StatusTreino)
* **Aplicação:** Transição do ciclo de vida do treino representado pela enumeração `StatusTreino` (`PRESCRITO`, `EM_EXECUCAO`, `CONCLUIDO`).
* **Propósito:** Encapsular os comportamentos específicos e as regras de transição que o treino assume quando passa de estipular/agendar para execução pelo aluno e posterior conclusão.

### Observer (para Notificações de Acompanhamento e Feedback)
* **Aplicação:** Notificação do Personal sobre ações do Aluno (como registrar feedback, concluir treino ou tirar dúvidas).
* **Propósito:** Atualizar a visão do Personal Trainer em tempo real ou gerar alertas quando um evento relevante do aluno for registrado no sistema.

### Strategy (para Cálculo e Gerenciamento de Mensalidades)
* **Aplicação:** Regras de pagamento e envio de parcelas.
* **Propósito:** Encapsular diferentes formas/estratégias de pagamento e regras de cobrança (ex.: Pix, Cartão, Boleto) utilizadas para gerenciar a situação da mensalidade do aluno.

---

## 4. Padrões Arquiteturais e de Persistência

### MVC (Model-View-Controller)
* **Aplicação:** Estruturação geral informada no documento de arquitetura.
* **Camadas:**
  * **Model (Modelo):** Contém os dados e a lógica de negócio (`Usuario`, `Aluno`, `Personal`, `TreinoAluno`, `ItemExercicio`, `Exercicio`, `Conta`).
  * **View (Visão):** Interfaces Java (como JavaFX) para interação do Personal e do Aluno.
  * **Controller (Controlador):** Intermedia as propostas das visões, acionando as regras de negócio do Modelo e atualizando a interface.

### DAO (Data Access Object) / Repositório
* **Aplicação:** Isolamento de acesso ao banco de dados relacional indicado na arquitetura.
* **Propósito:** Abstração do acesso e das operações CRUD para as entidades persistentes (`UsuarioDAO`, `TreinoDAO`, `ContaDAO`).

<img width="1281" height="1149" alt="Class Diagram0" src="https://github.com/user-attachments/assets/5c216452-a752-450b-9d33-a12ad88395c9" />
