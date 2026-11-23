# ORBIT-1 · implantação no wiki-br

Esta pasta reúne o codificador ORBIT-1 (frases UTF-8 → anéis binários → PNG → leitura). O arquivo `index.html` é independente e dispensa build, dependências e backend.

## Publicação

1. Copie `orbit/index.html` para a pasta pública do servidor wiki-br, preservando o nome `index.html`.
2. Configure uma rota estática (por exemplo, `https://www.wiki-br.duckdns.org/orbit/`) apontando para esse arquivo. Isso exige acesso ao repositório ou configuração do servidor real, que não está incluído aqui.
3. Verifique a página no navegador, digite uma frase UTF-8, salve o PNG composto, importe-o e confirme que a frase é recuperada.
4. Verifique que `/gh` e `/openapi.json` continuam respondendo como antes.

### Exemplo ilustrativo para Nginx

Para implantação em um diretório chamado `/var/www/wiki-br/orbit/`:

```nginx
location /orbit/ {
    alias /var/www/wiki-br/orbit/;
    index index.html;
    try_files $uri $uri/ =404;
}
```

Ajuste ao servidor existente e faça uma verificação da configuração antes de recarregá-la. Não substitua roteamentos ou configurações de autenticação já existentes.

## Segurança e escopo

- O texto é dado, não comando executável; não há execução nativa ou backdoor.
- Máscara XOR e rotação são recursos de representação, **não criptografia**.
- CRC32 verifica alterações acidentais, não garante autenticidade.
- O módulo não acessa a API, não publica mensagens e não altera o experimento da inscrição original.
- Fotos ou capturas de tela podem não ser decodificáveis; use o PNG original.
