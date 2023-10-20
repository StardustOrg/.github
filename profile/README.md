# StardustOrg :sparkles:

Bem-vindo ao repositório da StardustOrg, uma organização dedicada a abrigar os trabalhos desenvolvidos para a disciplina "Programação para Web I" do curso de Sistemas e Mídias Digitais da Universidade Federal do Ceará (UFC). Este repositório contém os projetos e atividades desenvolvidos por alunos ao longo do curso.

## Membros da Equipe :busts_in_silhouette:

| Nome             | Matrícula | Email                  |
|---------------------|-----------|------------------------|
| JOAO VICTOR BARROSO ALVES        | 509697    | joaovba2002@alu.ufc.br      |
| NICKOLAS GABRIEL LIMA RODRIGUES  | 509811    | nickolasgabriel@alu.ufc.br      |
| VLADIA HELEN FERREIRA FARIAS     | 511730    | vladiahelenff@gmail.com     |
| YANNA TORRES GONCALVES     | 507773    | torres.yanna03@gmail.com      |

Juntos, buscamos aplicar os conceitos e técnicas aprendidas para criar soluções web funcionais e utilizáveis.

## StardustCard :computer:

<div align="center">
   <img src="logo.svg" width="500">
</div>

<br>

O principal produto da organização StardustOrg é o e-commerce StardustCard, uma plataforma de vendas de Photocards de K-pop da mais alta qualidade. O StardustCard é uma janela para os colecionadores de photocards e fãs de K-pop, permitindo que estes adquiram Photocards autênticos sem necessidade de comprar os álbuns.
*A touch of Stardust*

### Tecnologias Utilizadas 🛠️

- **Prototipação:** Figma e Draw.io
- **Desenvolvimento Front-end:** HTML, CSS e JavaScript
- **Desenvolvimento Back-end:** Java (JSP e Servlet)
- **Banco de Dados:** PostgreSQL

### Entregas 📅

#### Entrega 01 (29/09/2023)

1. **Protótipo StardustCard** :memo:
   
   Descrição: Protótipo de alta fidelidade do e-commerce StardustCard, uma loja de photocards, para os perfis Cliente e Administrador.
   
   [Link para o Protótipo no Figma](https://www.figma.com/file/PJWhswW6SMbAIEF9cnT8bz/Stardust-%7C-Prot%C3%B3tipo?type=design&node-id=0%3A1&mode=design&t=noJvPYJ8AvP8BBOh-1)

2. **Modelo Banco de Dados** :card_index_dividers:
   
   Descrição: Modelagem do Banco de Dados Relacional (Modelo Entidade-Relacionamento e Modelo Relacional).

   - **MER:**
     
     ![Modelo Entidade-Relacionamento](stardust-mer02.png)

   - **Modelo Relacional:**
     
     ![Modelo Relacional](stardust-mr.png)
      
   Para a instanciação do banco, segue os seguinte script:
   * [Script de criação](https://github.com/StardustOrg/Database/blob/main/stardust_db_schema.sql)

4. **Front-end** :art:
   
   Descrição: Primeira versão do front-end do e-commerce em HTML, CSS e JavaScript.

   - [Repositório Front-end Cliente](https://github.com/StardustOrg/BasicHTML_Client)
   - [Repositório Front-end Admin](https://github.com/StardustOrg/BasicHTML_Admin)

#### Entrega 02 (23/10/2023)

1. **Diagrama de Classes** :pick:
   
2. **Camada 'Model' (MVC)** :clipboard:

3. **Funcionalidades**

  - **Cadastrar Novo Cliente**:
  - **Autenticar acesso (Login):**

4. **Remodelagem do Banco de Dados** :floppy_disk:

   Por fim, houve uma atualização no esquema de algumas tabelas, principalmente a tabela de *Categoria* (onde foi adicionado um novo campo, para guardar outra imagem).

   O novo script de instanciação do banco pode ser encontrado no seguinte arquivo: [Script de criação](https://github.com/StardustOrg/Database/blob/main/stardust_db_schema.sql)

   :exclamation: Recomendamos que o banco seja instanciado com o nome "stardust_db". Caso deseje usar outro nome, mude a referência na classe `Config`, no pacote `config` do código.

   :exclamation: No novo script de criação já vem incluido um usuário *admin* com as seguintes credenciais de acesso:

      - **login:** admin01
      - **senha:** 123456
