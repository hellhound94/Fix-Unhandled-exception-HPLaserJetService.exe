# Fix-Unhandled-exception-HPLaserJetService.exe
Here's a simple way to solve this problem using HP drivers for LaserJet printers.

Depois de eu instalar os drivers para minha impressora HP P1102W e possuir instalado na minha máquina o Visual Studio começou a aparecer a seguinte mensagem.

<p align="center">
  <img src="https://github.com/hellhound94/Fix-Unhandled-exception-HPLaserJetService.exe/blob/main/Captura%20de%20tela%202026-06-06%20132528.png" alt="mensagem de erro">
</p>

Versão do driver:
<p align="center">
  <img src="https://github.com/hellhound94/Fix-Unhandled-exception-HPLaserJetService.exe/blob/main/Captura%20de%20tela%202026-06-06%20141011.png" alt="Versão dos drivers">
</p>

Tentei desativar essa caixa de mensagem tanto no Visual Studio quanto no Windows porém sem sucesso.

Foi aí que decidi usar minhas experiências como Cracker.

Iniciei o debugger na primeira imagem que mostrei.

Então abriu o Visual Studio 2026
<p align="center">
  <img src="https://github.com/hellhound94/Fix-Unhandled-exception-HPLaserJetService.exe/blob/main/Captura%20de%20tela%202026-06-06%20132707.png" alt="debugger 1">
</p>

Verifiquei os detalhes
<p align="center">
  <img src="https://github.com/hellhound94/Fix-Unhandled-exception-HPLaserJetService.exe/blob/main/Captura%20de%20tela%202026-06-06%20132729.png" alt="debugger 2">
</p>
Pelas imagens vi que na função DoModelInfoGathering() está tendo uma exceção e que então o debugger do Visual Studio entra automaticamente.

## 🛠️ Passo a Passo da Solução

1. Abri no dnSpy .net o executável `HPLaserJetService.exe` localizado no diretório:
```text
C:\Program Files (x86)\HP\HPLaserJetService
```

<p align="center">
  <img src="https://github.com/hellhound94/Fix-Unhandled-exception-HPLaserJetService.exe/blob/main/Captura%20de%20tela%202026-06-06%20140617.png" alt="dnSpy">
</p>

2. Alterei a função `DoModelInfoGathering()` para retornar apenas `true`, pulando as instruções que causavam a exceção:

```csharp
protected override bool DoModelInfoGathering()
{
    // ...
    return true;
}
```

Dessa forma ao iniciar o Windows 11 sumiu para sempre esse problema.

Irei deixar o `HPLaserJetService.exe` com o patch para quem precisar apenas substituir o arquivo.

---

### ⚠️ Disclaimer / Aviso de Segurança
Este repositório fornece um arquivo executável (`.exe`) modificado por terceiros para corrigir um bug específico do driver HP. 
* O uso deste arquivo é por **sua conta e risco**.
* Recomenda-se fazer um **backup** do arquivo original antes de realizar a substituição.
* Caso prefira, você mesmo pode realizar o procedimento utilizando a ferramenta dnSpy seguindo o passo a passo descrito acima.

---

Obrigado por ler até aqui. Espero que a HP resolva logo esse bug. Até mais.
