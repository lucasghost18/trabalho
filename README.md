### AVISO, O README ABAIXO É APENAS PRÉVIO PARA NÓS DO GRUPO ENTENDERMOS COMO EU FIZ ATÉ AGORA E COMO FUNCIONA ESSA CACETA PRETA ###

### PROBLEMAS QUE PASSEI NESSE PROJETO: ###
- Tive de reinstalar o Git na minha nova máquina (notebook);
- Tive de reinstalar o Pytest pelo mesmo motivo do de cima;
- Pelo fato do meu código estar dentro de "src/consulta_cep/", o pytest não soube que o diretório src deveria entrar no PYTHONPATH. Para resolver isso precisei utilizar: 
``` $env:PYTHONPATH = "$PWD\src" ```
``` pytest -q ``` (Cê copia os dois aí sem os "```" e cola os 2 juntos no Terminal)
(Foi a forma que eu achei mais simples, do que ter de refazer os códigos)

### COMANDOS PARA A EXECUÇÃO DO PROJETO: ###
- Depois que você pegar o arquivo zip, você vai abrir ele no VsCode, abrir o terminal e então fazer:
``` python -m venv .venv ```
``` pip install -r requirements.txt ```
- Então ative o venv corretamente:
```  .\.venv\Scripts\Activate ```
- Instale o Pytest no ambiente virtual:
``` pip install pytest ```
- Prossiga:
``` $env:PYTHONPATH = "$PWD\src" ```
``` pytest -q ```
- Após certifica-se de que todos os 6 tenham passado, prossiga com os comandos utilizando o Git:
``` git add -A ```
``` git commit -m "feat: formatar_endereco_completo + testes com mocks" ```
``` git commit -m "chore(ci): add quality stage with flake8; enforce lint before tests" ```
- Caso surja o seguinte resultado:
``` On branch feature/formatar-endereco ``` 
``` nothing to commit, working tree clean ```
- Passe para o comando:
``` git push origin feature/formatar-endereco ```
- Ao final dele teremos dois "erros fatais": 
``` fatal: 'origin' does not appear to be a git repository ```
``` fatal: Could not read from remote repository. ```
- Não há alterações novas para serem commitadas (tudo já está salvo no Git) e o Projeto ainda não está conectado a um repositório remoto (no GitLab).
- Para passarmos a diante quais serão os próximos passos,  primeiro precisaremos conectar o Projeto ao Git usando o endereço do repositório do GitLab, usando o comando:
``` git remote add origin https://gitlab.com/seu-usuario/seu-repositorio.git ```
- Agora para a parte de conexão do repositório e finalização do projeto, precisamos ter em mente de utilizar comandos como:
``` git remote -v ```
(Para verificar se o repositório remoto foi adicionado corretamente)
``` git push -u origin feature/formatar-endereco ```
(Para adicionar todos os arquivos para o repositório remoto)
- Então, no GitLab, vamos precisar abrir um Merge Request da branch feature/formartar-endereco para a branch principal (main ou master [Acredito que seja master, mas pode ser que seja um engano]).
### Lembrete de adicionar a professora como colaboradora do projeto privado no GitLab após a finalização de tudo isso.
- Vamos aguardar então o Pipeline rodar automaticamente, com ele executando os stages: build > qualidade_codigo(flake8) > test (pytest).
- Se algum stage falhar, vamos precisar corrigir os probelmas localmente, commitando e dando push novamente.
- Assim que o pipeline ficar verde, todos os stages vão estar Ok (Funcionou).
- Vamos então fazer o merge da branch de feature para a principal e conferir se o código está atualizado na nossa branch principal.
### Lembrete de atualizar o README.md depois da conclusão do projeto. Explicando a nova função que escolhemos, os testes e o funcionamento do pipeline.

### SÓ PRA AJUDAR O CONDENADO QUE FOR FAZER ESSA CACETA DE CONEXÃO COM O REPOSITÓRIO (que bom que não sou você): ###
### Série de erros que podem acontecer nessa conexão com o repositório do GitLab e como resolver:


- Abrir um Merge Request da branch de feature para a principal.
> - Erro comum: MR não aparece ou não pode ser criado. 
> - Solução: Confirme se a branch foi enviada e se tem permissão no projeto.
- Aguardar o pipeline rodar automaticamente.
> - Erro comum: Pipeline falha no stage qualidade_codigo (flake8).
> - Solução: Corrija os avisos do flake8 (imports não usados, linhas longas, indentação, etc.) no código.
> - Erro comum: Pipeline falha no stage test (pytest).
> - Solução: Corrija os testes unitários, verifique se os mocks estão corretos e se o código está funcionando.
> - Erro comum: "ModuleNotFoundError" nos testes.
> - Solução: Verifique se o PYTHONPATH está correto no .gitlab-ci.yml e se a estrutura de pastas está certa.
- Após o pipeline ficar verde (todos os stages OK):
- Fazer o merge da branch de feature para a principal.
- Conferir se o código está atualizado na branch principal.
> - Erro comum: Merge bloqueado por problemas de pipeline.
> - Solução: Corrija os erros apontados pelo CI antes de tentar o merge.