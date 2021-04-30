# DevSecOps: Teste de aplicativos da web com Cypress e OWASP ZAP

1. [Cypress] (https://www.cypress.io) é uma estrutura de teste UI / E2E para aplicativos da web. Você conhece o Selênio? Cypress é mais incrível em todos os aspectos. [Veja o motivo em um artigo meu] (https://blog.codecentric.de/en/2020/10/cypress-ui-end2end-testing/)
2. [OWASP ZAP] (https://www.zaproxy.org/) é um verificador de segurança de aplicativos da web. Ele reúne o tráfego usando um proxy, explora mais, faz a varredura passiva e ativa de aplicativos da web em busca de vulnerabilidades potenciais.
3. [OWASP Juice Shop] (https://owasp.org/www-project-juice-shop/) é um aplicativo da web intencionalmente inseguro para fins de treinamento e educação.

## Porquê e como?
### Combinando duas ótimas ferramentas para um objetivo maior

Essas ferramentas podem ser combinadas de uma forma interessante. ** Cypress ** pode fazer proxy de todo o tráfego gerado durante a execução do teste por meio do ** OWASP ZAP **. O ZAP aprenderá aproximadamente quais sites o aplicativo da web em teste possui. Reúne alertas de segurança encontrados no trânsito. Depois disso, o ZAP também pode executar varreduras ativas no aplicativo. Eles tentam alguns ataques ativos contra o site, como injeções de SQL ou tentativas de Cross-Site-Scripting. Posteriormente, o OWASP ZAP fornece relatórios incluindo todas as vulnerabilidades encontradas.

### OWASP Juice Shop como aplicativo de demonstração

O famoso JS tem uma boa quantidade de vulnerabilidades sérias. Portanto, é perfeito para demonstrar que tipo de vulnerabilidades e cheiros podem ser descobertos com testes de clique automatizados e varredura ativa.

## Executando

### Localmente contra Juice Shop remota

Juice Shop já está funcionando em: https://juice-shop.herokuapp.com

Inicie o OWASP ZAP no modo headless usando Docker, pois precisamos apenas de sua API HTTP, em `http://localhost:8080`:


```bash
docker run -u zap -p 8080:8080 jverhoelen/owasp-zap-with-entrypoint
# esta imagem é uma variante de https://github.com/zaproxy/zaproxy/blob/develop/docker/Dockerfile-bare
# foi criado a partir do arquivo https://github.com/jverhoelen/zaproxy/blob/develop/docker/Dockerfile-bare-entrypoint
# ele apenas executa o ZAP como um ponto de entrada do Docker usando seu wrapper de script bash zap.sh com alguns argumentos padrão, de modo que se liga a 0.0.0.0:8080 como daemon sem chave de API
```


Configure o ZAP como proxy para o Cypress e execute os testes:

```bash
npm i

npm run remote:all
```
