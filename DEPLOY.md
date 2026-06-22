# 🚀 Guia de Deploy

## Opção 1: GitHub Pages (Gratuito)

1. **Faça upload do repositório para o GitHub**

2. **Configure as páginas do repositório:**
   - Vá para Settings → Pages
   - Selecione "Deploy from a branch"
   - Escolha a branch `main` e a pasta `/root`
   - Salve

3. **Acesse a landing em:**
   ```
   https://seu-usuario.github.io/salva-boni-landing
   ```

## Opção 2: Vercel (Gratuito, recomendado)

1. **Acesse** https://vercel.com

2. **Clique em "Import Project"**

3. **Conecte seu repositório GitHub**

4. **Vercel detectará automaticamente e fará o deploy**

5. **Seu site estará em:**
   ```
   https://salva-boni-landing.vercel.app
   ```

## Opção 3: Netlify (Gratuito)

1. **Acesse** https://netlify.com

2. **Faça login com GitHub**

3. **Clique "Add new site" → "Import an existing project"**

4. **Selecione o repositório**

5. **Deixe as configs padrão e clique "Deploy"**

6. **Site estará em:**
   ```
   https://salva-boni-landing.netlify.app
   ```

## Opção 4: Hospedagem Própria (Seu Servidor)

### Via FTP:
```bash
# Faça upload dos arquivos via FTP para seu servidor:
- index.html
- vitor.png
```

### Via SSH:
```bash
scp -r * seu-usuario@seu-servidor.com:/var/www/salva-boni/
```

### Via Git (se seu servidor suporta):
```bash
ssh seu-usuario@seu-servidor.com
cd /var/www/salva-boni
git clone https://github.com/seu-usuario/salva-boni-landing.git .
```

## Opção 5: Docker (Para mais controle)

Crie um arquivo `Dockerfile`:

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY vitor.png /usr/share/nginx/html/vitor.png

EXPOSE 80
```

Build e rode:
```bash
docker build -t salva-boni-landing .
docker run -p 80:80 salva-boni-landing
```

## Domínio Customizado

### GitHub Pages:
1. Settings → Pages → Custom Domain
2. Digite seu domínio (ex: salvaboni.com)
3. Crie um CNAME no seu DNS apontando para: `seu-usuario.github.io`

### Vercel/Netlify:
1. Vá para Settings/Domain Settings
2. Adicione seu domínio customizado
3. Configure os registros DNS conforme instruído

## 🔒 Certificado SSL

Se usar GitHub Pages, Vercel ou Netlify:
- ✅ SSL automático (HTTPS)
- ✅ Renovação automática
- ✅ Tráfico criptografado

## ⚡ Performance

Recomendações:
- Use **Vercel** ou **Netlify** para melhor performance
- Ambos oferecem CDN global gratuito
- Deploy automático a cada push no GitHub

## 📊 Analytics (Opcional)

### Google Analytics:
1. Crie uma conta em https://analytics.google.com
2. Obtenha seu Tracking ID (UA-XXXXXXXXX-X ou G-XXXXXXXXXX)
3. Adicione ao `<head>` do `index.html`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### Facebook Pixel:
Adicione ao `<head>`:

```html
<!-- Facebook Pixel -->
<script>
  !function(f,b,e,v,n,t,s)
  {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
  n.callMethod.apply(n,arguments):n.queue.push(arguments)};
  if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
  n.queue=[];t=b.createElement(e);t.async=!0;
  t.src=v;s=b.getElementsByTagName(e)[0];
  s.parentNode.insertBefore(t,s)}(window, document,'script',
  'https://connect.facebook.net/en_US/fbevents.js');
  fbq('init', 'SEU_PIXEL_ID');
  fbq('track', 'PageView');
</script>
<noscript><img height="1" width="1" style="display:none"
  src="https://www.facebook.com/tr?id=SEU_PIXEL_ID&ev=PageView&noscript=1"
/></noscript>
```

## 🆘 Troubleshooting

### Imagem (vitor.png) não aparece:
- Verifique se o arquivo `vitor.png` está na mesma pasta que `index.html`
- Verifique o nome do arquivo (case-sensitive em Linux)
- Limpe o cache do navegador (Ctrl+Shift+Delete)

### Layout quebrado:
- Limpe cache: Ctrl+Shift+Delete
- Recarregue a página: Ctrl+F5
- Tente em outro navegador

### Deploy não atualiza:
- Vercel/Netlify: Aguarde 1-2 min (redeployment automático)
- GitHub Pages: Limpe cache ou aguarde até 5 min
- Seu servidor: Limpe cache via SSH ou painel de controle

---

**Qualquer dúvida, consulte a documentação oficial da plataforma escolhida.**
