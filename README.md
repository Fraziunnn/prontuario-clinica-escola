# prontuario-clinica-escola

# Prontuário Eletrônico Inteligente para Clínicas-Escola

## 🩺 Sobre o Projeto

Este projeto apresenta o **protótipo de um Prontuário Eletrônico Inteligente (PEI)** desenvolvido para clínicas-escola, com integração ao **Supabase** e interface criada no **Lovable**.
O sistema permite o **cadastro de pacientes**, o **registro e acompanhamento de atendimentos** e a **edição das informações** com base em dados estruturados.

O objetivo é **modernizar o processo de documentação clínica**, reduzindo o tempo de registro manual, melhorando a qualidade dos dados e oferecendo suporte ao aprendizado supervisionado de estudantes da área da saúde.

---

## 🧱 Tecnologias Utilizadas

* **Lovable** – Criação da interface e integração com Supabase
* **Supabase** – Banco de dados PostgreSQL em nuvem
* **SQL** – Criação das tabelas, view e função
* **UUID** – Identificação única de registros
* **GitHub Pages / Lovable Deploy** – Hospedagem da aplicação

---

## 🗃️ Estrutura do Banco de Dados

### Tabelas

#### `pacientes`

| Campo           | Tipo      | Descrição                 |
| --------------- | --------- | ------------------------- |
| id              | UUID (PK) | Identificador único       |
| nome            | text      | Nome completo do paciente |
| data_nascimento | date      | Data de nascimento        |
| sexo            | text      | Sexo biológico            |
| telefone        | text      | Contato telefônico        |

#### `atendimentos`

| Campo                | Tipo      | Descrição                   |
| -------------------- | --------- | --------------------------- |
| id                   | UUID (PK) | Identificador único         |
| paciente_id          | UUID (FK) | Relacionamento com paciente |
| data_atendimento     | date      | Data do atendimento         |
| resumo_ia            | text      | Resumo automático da IA     |
| hipotese_diagnostica | text      | Hipótese diagnóstica        |
| conduta              | text      | Conduta médica              |

---

### View: `atendimentos_detalhados`

Mostra os atendimentos junto ao nome do paciente:

```sql
create or replace view atendimentos_detalhados as
select 
  a.id,
  p.nome as paciente_nome,
  a.data_atendimento,
  a.hipotese_diagnostica,
  a.conduta
from atendimentos a
join pacientes p on a.paciente_id = p.id;
```

---

### Função: `contar_atendimentos(paciente_uuid)`

Conta quantos atendimentos cada paciente possui:

```sql
create or replace function contar_atendimentos(paciente_uuid uuid)
returns integer
language sql
as $$
  select count(*) 
  from atendimentos 
  where paciente_id = paciente_uuid;
$$;
```

---

## 💻 Funcionalidades (CRUD Completo)

### Pacientes

* **Cadastrar** paciente (create)
* **Listar** pacientes (read)
* **Editar** informações (update)
* **Excluir** cadastro (delete)

### Atendimentos

* **Cadastrar** atendimento vinculado ao paciente
* **Listar** atendimentos usando a view `atendimentos_detalhados`
* **Editar** hipótese diagnóstica e conduta
* **Excluir** atendimento

---

## 🖼️ Prints das Telas

* Tela de Cadastro de Pacientes
* Tela de Listagem de Atendimentos
* Tela de Edição de Atendimento
  *(Inserir imagens exportadas do Lovable aqui)*

---

## 🌐 Link do Deploy

[🔗 Acessar Aplicação no Lovable](https://lovable.dev/projects/7212af2e-520b-4be3-84c3-b85e4d6f5ef8)

---

## 📦 Repositório

* [GitHub do Projeto](https://github.com/Fraziunnn/flow-assist-transcribe-11731.git)

---

## 🎓 Autoria

Desenvolvido por **Guilherme Frazão Feitoza**
Projeto acadêmico – Curso de Engenharia de Software – Centro Universitário Santo Agostinho (UNIFSA)
