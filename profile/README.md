# StardustOrg :sparkles:

Bem-vindo ao repositório da StardustOrg, uma organização dedicada a abrigar os trabalhos desenvolvidos para a disciplina "Programação para Web I" do curso de Sistemas e Mídias Digitais da Universidade Federal do Ceará (UFC). Este repositório contém os projetos e atividades desenvolvidos por alunos ao longo do curso.

**Sumário de entregas: [Entrega 01 (29/09/2023)](https://github.com/StardustOrg/.github/edit/main/profile/README.md#entrega-01-29092023) • [Entrega 02 (23/10/2023)](https://github.com/StardustOrg/.github/edit/main/profile/README.md#entrega-02-23102023)  • [Entrega 03 (17/11/2023)](#entrega-03-17112023) • [Entrega Final (*to do*)]() •**

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
- [Repositório Stardust Eccomerce](https://github.com/StardustOrg/StardustCard-Ecommerce.git)

1. **Diagrama de Classes** :pick:

   Para guiar o desenvolvimento do sistema, criamos um pequeno diagrama de classes relacionado a camada Model.

   ![Diagrama de Classes](stardust_card_class_diagram.png)
   
2. **Camada 'Model' (MVC)** :clipboard:

   Com base no diagrama de classes do item anterior, desenvolvemos toda a camada modelo que pode ser encontrada dentro do pacote `model` do [projeto](https://github.com/StardustOrg/StardustCard-Ecommerce/tree/main/src/java/model)

3. **Funcionalidades**

     - **Cadastrar Novo Cliente**:
       
          Para a realização dessa função partimos da criação de um formulário de cadastro que passa como `action` o caminho `/Register`:
         ```jsp
         <form method="POST" action="${pageContext.request.contextPath}/Register" onsubmit="return validateRegisterForm()">
           <h2>Create account</h2>
           <label>Your Name:</label>
           <input type="text" name="name" id="name" placeholder="First and last name" required>
           <label>Address:</label>
           <input type="text" name="address" id="address" placeholder="Your address" required>
           <label>Email:</label>
           <input type="email" name="email" id="email" placeholder="Your email" required>
           <label>Login:</label>
           <input type="text" name="login" id="login" placeholder="At least 6 characters" required>
           <label>Password:</label>
           <input type="password" name="password" id="password" placeholder="At least 6 characters" required>
           <label>Confirm Password:</label>
           <input type="password" name="confirm-password" id="confirm-password" placeholder="Repeat your password"
                  required>
           <button>Register</button>
         </form>
         ```
         Esta action aciona a `RegisterServlet` que em seu método POST recupera os dados de cadastro e utiliza o `UserDAO` para inserir os dados no banco, se o cadastro der certo ele redireciona para a Tela de Login, se não deu certo ele dá um aviso de erro e permanece na tela de Register:
         ```java
            protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
              String login = request.getParameter("login");
              String email = request.getParameter("email");
              boolean admin = Boolean.parseBoolean(request.getParameter("admin"));
              String password = request.getParameter("password");
              String address = request.getParameter("address");
              String name = request.getParameter("name");
            
              User user = new User(login, password, email, admin, address, name);
              UserDAO userDAO = new UserDAO();
              boolean cadastrado = userDAO.insert(user);
            
              if (cadastrado) {
                  response.sendRedirect("Login");
              } else {
                  String alertMessage = "Registration failed. Please try again.";
                  String redirectScript = "<script>alert('" + alertMessage + "'); window.location.href = 'Register';</script>";
                  response.getWriter().write(redirectScript);
              }
            }
         ```

     - **Autenticar acesso (Login):**
      
         Para a realização dessa função partimos da criação de um formulário de login que passa como `action` o caminho `/Login`:
         ```jsp
          <form method="POST" action="${pageContext.request.contextPath}/Login" onsubmit="return validateLoginForm()">
              <h2>Sign in</h2>
              <label>Login:</label>
              <input type="text" name="login" id="login" placeholder="Login" required>
              <label>Password:</label>
              <input type="password" name="password" id="password" placeholder="Password" required>
              <a class="text_link">Forgot password?</a>
              <button>Sign In</button>
          </form>
         ```
         Este action aciona a `LoginServlet` que posui um método POST que recupera os dados de login e usa o `UserDAO` para verificar no banco se aqueles dados existem. Se existirem a Servlet cria variáveis de sessão para armazenar dados do usuário. Após isso, a servlet redireciona o usuário para a tela correspondente a seu tipo de usuário, caso ele seja administrador leva para a tela de `Admin`, caso contrário, para a tela de `Home`.
       ```java
          protected void doPost(HttpServletRequest request, HttpServletResponse response)
               throws ServletException, IOException {
           String login = request.getParameter("login");
           String password = request.getParameter("password");
         
           UserDAO userDAO = new UserDAO();
           boolean success = userDAO.validateAccess(login, password);
           response.setContentType("text/html;charset=UTF-8");
           if (success) {
               User myUser = userDAO.getOne(login);    
               /**
                * Cria uma sessão de usuário com Login, Nome se o usuário é Admin
                */
               HttpSession session = request.getSession();
               session.setAttribute("login", myUser.getLogin());
               session.setAttribute("name", myUser.getName());
               session.setAttribute("isAdmin", myUser.isAdmin());
         
               if (myUser.isAdmin()) {
                   response.sendRedirect("Admin");
               } else {
                   response.sendRedirect("Home");
               }
           } else {
               String alertMessage = "Login failed. Wrong Login/Password. Please try again.";
               String redirectScript = "<script>alert('" + alertMessage + "');  window.location.href = 'Login';</script>";
               response.getWriter().write(redirectScript);
           }
         }
       ```
         Por fim, protegemos as rotas das telas de Admin, uma vez que essas telas não podem ser acessadas a não ser que o usuário esteja autenticado como administrador, por meio de um Servlet que redireciona para a página, porém antes de redirecionar verifica a Sessão para ver se o usuário autenticado é um administrador:
       ```java
         @Override
         protected void doGet(HttpServletRequest request, HttpServletResponse response)
               throws ServletException, IOException {
           RequestDispatcher dispatcher = request.getRequestDispatcher("/admin/index.jsp");
           dispatcher.forward(request, response);
         }
       ``` 

4. **Remodelagem do Banco de Dados** :floppy_disk:

   Por fim, houve uma atualização no esquema de algumas tabelas, principalmente a tabela de *Categoria* (onde foi adicionado um novo campo, para guardar outra imagem).

   O novo script de instanciação do banco pode ser encontrado no seguinte arquivo: [Script de criação](https://github.com/StardustOrg/Database/blob/main/stardust_db_schema.sql)

   :exclamation: Recomendamos que o banco seja instanciado com o nome "stardust_db". Caso deseje usar outro nome, mude a referência na classe `Config`, no pacote `config` do código.

   :exclamation: No novo script de criação já vem incluido um usuário *admin* com as seguintes credenciais de acesso:

      - **login:** admin01
      - **senha:** 123456

#### Entrega 03 (17/11/2023)

- [Repositório Stardust Eccomerce](https://github.com/StardustOrg/StardustCard-Ecommerce.git)

A partir dessa entrega, o desenvolvimento do sistema fica focado na resolução de issues, que aqui representam os requisitos, bugs e melhoramentos do sistema. Ao todo, foram resolvidas 15 issues, divididas entre features do cliente, admin, melhorias e modificações no banco de dados.

<details>
  <summary><b>Melhorias</b></summary>

   Só houve uma issue de melhoria que é: [Mapeamento de Erros para páginas específicas #32](https://github.com/StardustOrg/StardustCard-Ecommerce/issues/32) Essa issue consiste em enviar um feedback visual para o usuário do sistema e também esconder a stack de erros. 
   
   Foram mapeados os principais HTTP status que representam erro: 404 (Page Not Found), 403 (Forbidden), 500 (Internal Server Error) e 503 (Service Unavailable). Cada um possui seu servlet adquado e página, com indicações do que fazer.

   ```xml
    <error-page>
        <error-code>404</error-code>
        <location>/404</location>
    </error-page>
    <error-page>
        <error-code>403</error-code>
        <location>/403</location>
    </error-page>
    <error-page>
        <error-code>500</error-code>
        <location>/500</location>
    </error-page>
    <error-page>
        <error-code>503</error-code>
        <location>/503</location>
    </error-page>
   ```

   ![Error Pages](error_pages.png)
  
</details>
<br>
<details>
  <summary><b>Banco de Dados</b></summary>

  Nessa entrega pequena atualização do banco de dados, a mudança do tipo da coluna `price` da tabela `product` (money &#10140; numeric).

  Houve a tentativa de adicionar uma nova tabela para mapear os lançamentos dos artistas - como 'sub-categorias' -, mas isso foi descartado pela complexidade que iria ser inserida dentro do sistema (repameamento dos servlets já existentes, atualização do diagrama de classes e DAOs).

  Você pode encontrar os scripts de definição do schema do banco e da instância no repositório **[Database](https://github.com/StardustOrg/Database/)**.

  :exclamation: Recomendamos que o banco seja instanciado com o nome "stardust_db". Caso deseje usar outro nome, mude a referência na classe `Config`, no pacote `config` do código.

</details>
<br>
<details>
  <summary><b>Features: Cliente</b></summary>

  Ao todo, foram finalizadas 8 issues relacionadas ao perfil e interface do cliente, incluindo a finalização do processo de LogOut.

  1. **Alteração de Cadastro e Exclusão de Cadastro:**
      
      Você pode acessar essa funcionalidade pelo servlet `/Profile`, porém é necessário que você esteja logado com uma conta válida do perfil 'client'. Quando esse Servlet é chamado, a função `doGet` carrega as informações pessoais e carrega também a página.

      ```java
        @Override
        protected void doGet(HttpServletRequest request, HttpServletResponse response)
                throws ServletException, IOException {
            HttpSession session = request.getSession(true);
            User user = (User) session.getAttribute("stardust_user");
            if (user != null && user.isAdmin() == false) {
                request.setAttribute("user", user);
                RequestDispatcher dispatcher = request.getRequestDispatcher("/client/profile_page.jsp");
                dispatcher.forward(request, response);
            } else {
                response.sendError(HttpServletResponse.SC_FORBIDDEN, "Don't have access");
            }
        }
      ```

      ```jsp
        <div class="profile-info-cont">
            <h3>Your information</h3>
            <div class="info-row">
                <div class="info-subt">
                    <p>This is your personal information. If you want to update, change the specific value and the
                        save it.</p>
                    <div id="delete-account" onclick="confirmDelete()">DELETE ACCOUNT</div>
                </div>
                <div class="details-form">
                    <form method="post">
                        <label>Your Name:</label>
                        <input type="text" name="name" id="name" placeholder="First and last name" value="<%= myUser.getName()%>" required>
                        <label>Address:</label>
                        <input type="text" name="address" id="address" placeholder="Your address" value="<%= myUser.getAddress()%>" required>
                        <label>Email:</label>
                        <input type="email" name="email" id="email" placeholder="Your email" value="<%= myUser.getEmail()%>" required>
                        <button>Save</button>
                    </form>
                </div>
            </div>
        </div>
      ```

      Caso o usuário escolha atualizar seu cadastro, ao submeter o formulário com as novas informações é realizada uma requisição para o mesmo Servlet, mas para método `POST`.

      ```java
        @Override
        protected void doPost(HttpServletRequest request, HttpServletResponse response)
                throws ServletException, IOException {
            response.setContentType("text/html;charset=UTF-8");
            HttpSession session = request.getSession(true);
            User user = (User) session.getAttribute("stardust_user");
            String name = request.getParameter("name");
            String address = request.getParameter("address");
            String email = request.getParameter("email");

            UserDAO userDAO = new UserDAO();
            if (user != null && user.isAdmin() == false) {
                User updatedUser = user;
                updatedUser.setAddress(address);
                updatedUser.setEmail(email);
                updatedUser.setName(name);
                boolean result = userDAO.update(updatedUser);
                if (result) {
                    session.setAttribute("stardust_user", updatedUser);
                response.sendRedirect("Profile");
                }
            } else {
                response.sendError(HttpServletResponse.SC_FORBIDDEN, "Don't have access");
            }
        }
      ```

      Caso o usuário queira excluir sua conta, primeiramente se chama a função JavaScript de confirmação da ação `confirmDelete()` e, caso a pessoa queira realmente excluir a conta, um Servlet específico de exclusão `/DeleteAccount`.

      ```javascript
        function confirmDelete() {
            var confirmation = confirm("Are you sure you want to delete your account?");
            if (confirmation) {
                window.location.href = "DeleteAccount";
            }
        }
      ```

      ```java
        @Override
        protected void doGet(HttpServletRequest request, HttpServletResponse response)
                throws ServletException, IOException {
            HttpSession session = request.getSession(true);
            User user = (User) session.getAttribute("stardust_user");
            if (user != null && user.isAdmin() == false) {

                UserDAO userDAO = new UserDAO();

                boolean delete = userDAO.delete(user.getId());
                if (delete) {
                    session.invalidate();
                    String alertMessage = "Account Deleted";
                    String redirectScript = "<script>alert('" + alertMessage + "'); window.location.href = 'Login';</script>";
                    response.getWriter().write(redirectScript);
                } else {

                    response.sendRedirect("Profile");
                }
            } else {
                response.sendRedirect("Login");
            }
        }
      ```

  2. **Listagem de Categorias (Artistas):**

      Como no protótipo apresentado na primeira entrega, a navegação é feita, geralmente, pelas categorias &#8212; que aqui são os artistas ou grupos.

      Assim, temos as seguintes páginas que são conectadas aos artistas: Page Incial, Página de Artistas, Páginas de um grupo e Páginas de um Artista/Membro.

      a. **_Home:_**
      
        A página inicial é acessada pelo Servlet `/Home` e através do método `doGet` é carregado todas as informações necessárias:

        ```java
            @Override
            protected void doGet(HttpServletRequest request, HttpServletResponse response)
                    throws ServletException, IOException {
                /*
                rest of the code
                */
                
                // list of artists
                ArtistDAO artistDAO = new ArtistDAO();
                
                List<Artist> artistsList = new ArrayList();
                try {
                    artistsList = artistDAO.getSoloArtistsAndGroups();
                } catch (Exception ex) {
                }
                request.setAttribute("artistsList", artistsList);

                /*
                rest of the code
                */
                
                RequestDispatcher dispatcher = request.getRequestDispatcher("/client/home.jsp");
                dispatcher.forward(request, response);
            }
        ```

        ```html
            <div class="bundles" id="artists">
                <h2>artists</h2>
                <div class="carrousel-container">
                    <span class="material-symbols-rounded" onclick="moveCarousel(-1)">
                        arrow_back_ios_new
                    </span>
                    <div class="carrousel">
                        <%
                            List<Artist> artistList = (List<Artist>) request.getAttribute("artistsList");
                            for (int i = 0; i < artistList.size(); i++) {
                                Artist artist = artistList.get(i);
                        %>
                        <a href="Artists/<%= artist.getName()%>" style="margin: 0 auto;">
                            <div class="artist-card">
                                <div class="artist-image">
                                    <img src="<%= artist.getIcon()%>" />
                                    <div class="overlay"></div>
                                    <div class="image-caption">
                                        <%= artist.getName()%>
                                    </div>
                                </div>
                            </div>
                        </a>
                        <%                            }
                        %>
                    </div>
                    <span class="material-symbols-rounded" onclick="moveCarousel(1)">
                        arrow_forward_ios
                    </span>
                </div>
            </div>
        ```
      
      b. **_Artists Page:_**
      
        A página que lista todos os artistas pode ser acessada pelo Servlet `/Artists` e através do método `doGet` carrega todos os artistas cadastrados no banco de dados.

        ```java
          @Override
          protected void doGet(HttpServletRequest request, HttpServletResponse response)
                  throws ServletException, IOException {
              /*
                rest of the code
              */
              ArtistDAO artistDAO = new ArtistDAO();
              
              List<Artist> artistsList = new ArrayList();
              try {
                  artistsList = artistDAO.getSoloArtistsAndGroups();
              } catch (Exception ex) {
              }
              request.setAttribute("artistsList", artistsList);
              
              /*
                rest of the code
              */
              
              RequestDispatcher dispatcher = request.getRequestDispatcher("/client/all_artists_page.jsp");
              dispatcher.forward(request, response);
          }
        ```

        ```html
            <% List<Artist> artistList = (List<Artist>) request.getAttribute("artistsList");
            %>
            <div class="bundles" id="artists">
                <h2>artists</h2>
                <div class="artists-container" id="all-artists">
                    <%                        for (int i = 0; i < artistList.size(); i++) {
                            Artist artist = artistList.get(i);
                    %>
                    <a href="Artists/<%= artist.getName()%>" style="width: 155px;">
                        <div class="artist-card">
                            <div class="artist-image">
                                <img src="<%= artist.getIcon()%>" />
                                <div class="overlay"></div>
                                <div class="image-caption">
                                    <%= artist.getName()%>
                                </div>
                            </div>
                        </div>
                    </a>
                    <%                            }
                    %>
                </div>
            </div>
        ```
      
      c. **_Artist Page:_**
      
        A página que lista todos os artistas pode ser acessada pelo Servlet `/Artists/*` e o método `doGet` separa o restante da url para identificar o artista ou grupo que se quer acessar.

        ```java
            @Override
            protected void doGet(HttpServletRequest request, HttpServletResponse response)
                    throws ServletException, IOException {
                request.setCharacterEncoding("UTF-8");
                /*
                  rest of the code
                */
                List<Artist> idols;
                ArtistDAO artistDAO = new ArtistDAO();
                String[] pathInfo = request.getPathInfo().split("/");

                switch (pathInfo.length) {
                    case 2 -> {
                        // Case: Artists/artist_slug
                        String artistSlug = pathInfo[1];
                        Artist artist = artistDAO.getBySlug(artistSlug);
                        if (artist != null && artist.getCover() != null) {
                            request.setAttribute("artistInfo", artist);
                            idols = artistDAO.getAllIdols(artist.getId());
                            if (idols.isEmpty()) {
                                request.setAttribute("group", false);
                            } else {
                                request.setAttribute("group", true);
                                Collections.sort(idols, Comparator.comparingLong(Artist::getId));
                                request.setAttribute("idols", idols);
                            }
                            /*
                              rest of the code
                            */
                        } else {
                            response.sendError(HttpServletResponse.SC_NOT_FOUND, "Artist not found");
                            return;
                        }
                    }
                    case 3 -> {
                        // Case: Artists/group_slug/member_slug
                        String groupSlug = pathInfo[1];
                        String memberSlug = pathInfo[2];
                        Artist group = artistDAO.getBySlug(groupSlug);
                        Artist member = artistDAO.getGroupMemberBySlug(group.getId(), memberSlug);
                        if (member != null && member.getCover() != null) {
                            request.setAttribute("artistInfo", member);
                            request.setAttribute("group", false);
                            /*
                              rest of the code
                            */
                        } else {
                            response.sendError(HttpServletResponse.SC_NOT_FOUND, "Artist not found");
                            return;
                        }
                    }
                    default -> {
                        // Invalid URL format, handle accordingly (e.g., show an error page)
                        response.sendError(HttpServletResponse.SC_NOT_FOUND, "Invalid URL format");
                        return;
                    }
                }

                RequestDispatcher dispatcher = request.getRequestDispatcher("/client/artist_page.jsp");
                dispatcher.forward(request, response);
            }
        ```

        ```html
            <%
                Artist artist = (Artist) request.getAttribute("artistInfo");
            %>
            <div class="cover">
                <img src="<%= artist.getCover()%>" />
                <div class="cover-caption">
                    <%= artist.getName()%>
                </div>
            </div>
            <!-- Rest of the code -->
            if (group) {
            %>
            <div class="bundles" id="members">
                <h2>members</h2>
                <div class="artists-container">
                    <%
                        List<Artist> artistList = (List<Artist>) request.getAttribute("idols");
                        for (int i = 0; i < artistList.size(); i++) {
                            Artist member = artistList.get(i);
                    %>
                    <a href="<%= artist.getName()%>/<%= member.getName()%>" style="width: 155px;">
                        <div class="artist-card">
                            <div class="artist-image">
                                <img src="<%= member.getIcon()%>" />
                                <div class="overlay"></div>
                                <div class="image-caption">
                                    <%= member.getName()%>
                                </div>
                            </div>
                        </div>
                    </a>
                    <%                            }
                    %>
                </div>
            </div>
            <%
                }
            %>
        ```

  3. **Página do produto:**

      Também de acordo com o protótipo, basicamente todas as páginas possuem uma listagem de produtos. Todos os Servlets apresentados no tópico anterior, além de carregar as informações dos artistas, carrega também informações dos produtos. Na página inicial, os produtos são carregados sem filtro de artista e no restante das páginas há um filtro.

      A fim de tentar apresentar para o usuário uma URL que não transpareça nenhuma informação direta do banco ou de como acessar, é criado uma sequência aleatória de caracteres, para cada formulário através do método `generateRandomSequence()` da classe `RandomSequenceGenerator`.

      ```java
        public class RandomSequenceGenerator {
            private static final String CHARACTERS = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

            public static String generateRandomSequence(int length) {
                StringBuilder randomSequence = new StringBuilder(length);
                SecureRandom secureRandom = new SecureRandom();

                for (int i = 0; i < length; i++) {
                    int randomIndex = secureRandom.nextInt(CHARACTERS.length());
                    char randomChar = CHARACTERS.charAt(randomIndex);
                    randomSequence.append(randomChar);
                }

                return randomSequence.toString();
            }
        }
      ```

      Exemplo de uso:

      ```html
          <div class="bundles" id="new-additions">
              <h2>new additions</h2>
              <div class="photocards">
                  <%
                      List<Product> newAdds = (List<Product>) request.getAttribute("newAdds");
                      int k = 6;
                      if (newAdds.size() < 6) {
                          k = newAdds.size();
                      }
                      for (int i = 0; i < k; i++) {
                          Product product = newAdds.get(i);
                          String uri = RandomSequenceGenerator.generateRandomSequence(15);
                  %>
                  <form id="formNA_<%= i%>" method="POST" action="${pageContext.request.contextPath}/Artists/Product/<%= uri%>" class="photocard-form">
                      <input type="hidden" name="productId" value="<%= product.getId()%>">
                      <div class="card" onclick="submitForm('formNA_<%= i%>')">
                          <div id="photo">
                              <img src="<%= product.getPicture()%>" alt="Avatar">
                          </div>
                          <div class="card-title"><%= product.getDescription()%></div>
                      </div>
                  </form>
                  <%                            }
                  %>  
              </div>
          </div>
      ```

      Para se acessar a página do produto, é chamado o Servlet `/Artists/Product/*`. Diferentemente dos outros Servlets que podem ser acessados pelo método `GET`, este só pode ser acessado pelo método `POST`, através dos formulários presentes em cada página.

      ```java
        @Override
        protected void doPost(HttpServletRequest request, HttpServletResponse response)
                throws ServletException, IOException {

            long id = Long.parseLong(request.getParameter("productId"));
            ProductDAO productDAO = new ProductDAO();
            Product product;
            try {
                product = productDAO.getOne(id);
                System.out.println(product.getId());
                request.setAttribute("product", product);
            } catch (Exception ex) {
                response.sendError(HttpServletResponse.SC_INTERNAL_SERVER_ERROR, "Something Happened");
            }
            
            // list of recently added or modified products
            List<Product> newAdds = new ArrayList();
            try {
                newAdds = productDAO.getRecommended(id);
                Collections.reverse(newAdds);
            } catch (Exception ex) {
            }
            request.setAttribute("newAdds", newAdds);

            RequestDispatcher dispatcher = request.getRequestDispatcher("/client/product_page.jsp");
            dispatcher.forward(request, response);
        }
      ```

</details>
<br>
<details>
  <summary><b>Features: Admin</b></summary>

   
</details>
<br>


#### Entrega Final (*to do*)
