# Análise de Tráfego: HTTP vs HTTPS 🦈

Este laboratório prático demonstra a vulnerabilidade do protocolo HTTP na transmissão de credenciais. O objetivo foi interceptar o tráfego de rede e capturar dados sensíveis em texto claro (*Clear Text*) utilizando o Wireshark.

## 🎯 Objetivo do Lab
Validar conceitos de **Sniffing** e a importância da criptografia (TLS) em aplicações web. A análise foca em identificar credenciais trafegando sem proteção na camada de aplicação.

## 🛠️ Ferramentas
* **Wireshark:** Captura e análise de pacotes.
* **Target:** `testphp.vulnweb.com` (Aplicação vulnerável autorizada para testes).
* **Filtros:** `http.request.method == POST` para isolar o envio de formulários.

## 📸 Evidência da Captura
A imagem abaixo comprova a interceptação bem-sucedida. Note os campos `uname` e `pass` visíveis no painel "HTML Form URL Encoded":

![Evidência do Wireshark](evidence.png)

## 🧠 Análise Técnica
1.  **Interceptação:** Como o HTTP não possui camada de criptografia (SSL/TLS), qualquer nó na rede (MITM) pode ler o *payload* TCP.
2.  **Método POST:** Identifiquei que, embora os dados não estejam na URL (como no GET), eles residem no corpo da requisição e são triviais de extrair.
3.  **Conclusão:** A única mitigação eficaz é a implementação de HTTPS, que tornaria este payload ilegível.

---
*Disclaimer: Este projeto foi realizado em ambiente controlado para fins educacionais.*
