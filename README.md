# 🍔 MamaFood - Sistema de Delivery

Sistema completo de delivery de comida com painel administrativo e área de pedidos.

## 🚀 Recursos

- ✅ **Login automático por email** - Entre apenas com seu email, sem senha
- 🎨 **Interface moderna** - Design inspirado no iFood, responsivo para mobile
- 👨‍💼 **Painel administrativo** - Gerencie pedidos, cardápio e histórico
- 📱 **100% Responsivo** - Funciona perfeitamente em celular, tablet e desktop
- 🔒 **Sistema de permissões** - Admin e usuário comum
- 🗺️ **Cálculo de taxa de entrega** - Com OpenRouter IA e mapas Leaflet
- 📦 **LocalStorage** - Dados salvos localmente no navegador

## 📂 Estrutura

```
├── Site Htmls/           # Páginas HTML
│   ├── Tela1.html       # Login/Cadastro
│   ├── Tela2.html       # Dashboard principal
│   ├── cardapio.html    # Visualizar cardápio
│   ├── cardapio-criar.html  # Criar produtos (admin)
│   ├── meus-pedidos.html    # Pedidos do usuário
│   ├── pedidos.html     # Gerenciar pedidos (admin)
│   ├── historico.html   # Histórico (admin)
│   ├── perfil.html      # Perfil da loja
│   └── taxa-entrega.html # Calcular entrega
├── App Js/              # Scripts
│   ├── shared.js        # Funções compartilhadas
│   └── app.js           # Script principal
├── Css/                 # Estilos
├── shared.css           # Estilos globais do painel
├── .env                 # Configurações (emails admin, chaves API)
└── index.html           # Página inicial (redireciona)
```

## 🔧 Configuração

### Definir administradores

Edite o arquivo `.env` e adicione os emails dos administradores:

```env
ADMIN_EMAILS=seu@email.com,outro@email.com
```

### Configurar localização da loja

No arquivo `.env`, ajuste as coordenadas da sua loja:

```env
LOJA_RUA=Rua São Vicente de Paula
LOJA_NUMERO=310
LOJA_CIDADE=Santa Juliana
LOJA_ESTADO=MG
LOJA_LAT=-19.3147
LOJA_LNG=-47.5291
```

## 🌐 Deploy

### GitHub Pages

1. Crie um repositório no GitHub
2. Faça upload de todos os arquivos
3. Vá em **Settings** > **Pages**
4. Selecione **main branch** como source
5. Pronto! Seu site estará em `https://seu-usuario.github.io/nome-repositorio`

## 👤 Como usar

### Primeiro acesso (novo usuário)

1. Acesse o site
2. Digite seu email
3. Preencha seus dados completos
4. Cadastro concluído! Você será redirecionado para o painel

### Acesso posterior (usuário existente)

1. Acesse o site
2. Digite seu email
3. ✅ **Login automático** - Você entra direto no painel!

## 🔐 Permissões

- **Usuário comum**: Cardápio, Meus Pedidos, Taxa de Entrega, Perfil
- **Administrador**: Todas as opções + Pedidos Ativos, Histórico, Criar Cardápio

## 📱 Mobile

O site é 100% responsivo:
- Sidebar deslizante
- Cards adaptados
- Formulários otimizados
- Mapas responsivos

## 🛠️ Tecnologias

- HTML5 / CSS3 / JavaScript (Vanilla)
- Font Awesome (ícones)
- Leaflet (mapas)
- ViaCEP (busca de endereço)
- OpenRouter AI (cálculo de entrega)
- LocalStorage (persistência)

## 📄 Licença

Projeto pessoal - Casa da Mama Hamburgueria

---

Desenvolvido com ❤️ para **Casa da Mama** 🍔
