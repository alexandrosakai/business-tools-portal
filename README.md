# 🧰 business-tools-portal

**Portal estático com ferramentas prontas para o dia a dia de uma empresa: checklists, diagnóstico, etiquetas e conferência de impostos. Sem build e sem banco de dados.**

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-F7DF1E?logo=javascript&logoColor=black)
![nginx](https://img.shields.io/badge/nginx-009639?logo=nginx&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-ready-2496ED?logo=docker&logoColor=white)

Uma página inicial com atalhos e várias ferramentas que rodam inteiramente no navegador. Basta servir os arquivos com qualquer servidor web.

## ✨ Funcionalidades

- **Portal inicial** com cartões de atalho para os seus sistemas
- **Checklists** de veículos, máquinas e rotinas, instaláveis como app (PWA)
- **Diagnóstico empresarial** com módulos de avaliação, plano de ação e exportação em JSON
- **Gerador de etiquetas** com código de barras, para impressão em lote
- **Conferência de impostos**: compara relatórios e aponta divergências entre notas
- **Painéis de operação do WhatsApp**: contatos, mensagens, pausa e teste (para uso com o [whatsapp-bot-stack](../whatsapp-bot-stack))

## 🧰 Tecnologias

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![nginx](https://img.shields.io/badge/nginx-009639?logo=nginx&logoColor=white)

HTML · CSS · JavaScript · Service Worker (PWA) · Chart.js, SheetJS, pdf.js, jsPDF, JsBarcode e mammoth (via CDN) · nginx

## 📋 Requisitos

- **Com Docker:** Docker e Docker Compose v2
- Acesso à internet nos navegadores (as bibliotecas vêm de CDN)
- **Sem Docker:** qualquer servidor de arquivos estáticos (nginx, Apache, Caddy, `python3 -m http.server`)

## 🚀 Instalação

### Com Docker

```bash
git clone https://github.com/alexandrosakai/business-tools-portal.git
cd business-tools-portal
cp .env.example .env        # opcional: muda a porta (WEB_PORT)
docker compose up -d --build
```

Abra `http://127.0.0.1:8080`.

### Sem Docker

```bash
# teste rápido
python3 -m http.server 8080
```

Em produção, copie os arquivos para a raiz do site e use, por exemplo, nginx:

```nginx
server {
    server_name portal.example.com;
    root /var/www/portal;
    index index.html;
    location / { try_files $uri $uri/ =404; }
}
```

Depois ative HTTPS: `sudo certbot --nginx -d portal.example.com`.

## ⚙️ Configuração

Não há segredos. Ajuste:

- **Links dos cartões** em `index.html` (os endereços `example.com` e `127.0.0.1` são exemplos)
- **WEB_PORT** no `.env`, para mudar a porta local do Docker
- **Imagens**: este repositório não traz logo nem ícones. Coloque os seus em `img/` e `checklist/` com os nomes `PLACEHOLDER-*.png` (veja os arquivos `IMAGENS-LEIA-ME.txt`)

## 🧭 Como usar

Abra a página inicial e escolha uma ferramenta. As telas de **WhatsApp** conversam com a API do `whatsapp-bot-stack`; as demais funcionam sozinhas, guardando dados no navegador.

## 📁 Estrutura de pastas

```
business-tools-portal/
├── index.html             # portal inicial
├── checklist/             # checklists (PWA: manifest.json, sw.js)
├── diagnostico/           # diagnóstico empresarial
├── etiquetas/             # gerador de etiquetas
├── conferencia-imposto/   # conferência de notas
├── whatsapp/              # painéis de operação do WhatsApp
├── img/                   # coloque aqui seu logo e favicon
├── Dockerfile
└── docker-compose.yml
```

## 🗺️ Roadmap

- [ ] Tema claro/escuro configurável
- [ ] Textos traduzidos (inglês e espanhol)
- [ ] Testes automatizados de interface
- [ ] Empacotar as ferramentas como um único app instalável (PWA)
- [ ] Exportação em PDF no diagnóstico

## 🤝 Como contribuir

1. Faça um fork e crie uma branch: `git checkout -b minha-melhoria`
2. Faça mudanças pequenas e focadas
3. Abra um Pull Request descrevendo o que mudou e como testar

## 📄 Licença

Distribuído sob a licença MIT. Veja o arquivo [LICENSE](LICENSE).
