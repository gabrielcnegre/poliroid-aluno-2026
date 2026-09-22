# Resolução do exercício 01: publicação

## Objetivo e base pronta

O formulário coordena seleção, envio temporário ao MinIO e confirmação do post pela API. Validação, campos visuais, diálogo e contratos já estavam prontos.

## Contratos consultados

Foram consultados , , , ,  e .

## Fluxo

1. Valida arquivo e legenda.
2. Solicita autorização e envia o arquivo ao staging privado.
3. Confirma o  com a legenda normalizada.
4. Em sucesso, limpa o formulário e chama .
5. Em falha de confirmação recuperável, preserva  e legenda para repetir somente a confirmação.
6. Em falha que exige novo upload, informa o usuário e permite selecionar outra imagem.

A ref  impede cliques duplicados antes da próxima renderização. O estado  informa progresso e mantém o diálogo fechado. A submissão preservada permite repetição idempotente no servidor.

## Estados e recuperação

Sucesso mostra confirmação, limpa arquivo e legenda e atualiza feed e galeria. Durante a operação o botão mostra “Publicando…” e o diálogo fica bloqueado. Falhas são anunciadas; a tentativa permanece quando a confirmação pode ser repetida. Nova seleção limpa mensagens antigas. Entrada inválida não inicia chamadas de rede.

## Verificação manual reproduzível

Em , abrir “Nova publicação”, selecionar imagem válida, preencher legenda e publicar. Confirmar autorização, upload e confirmação; abrir  e conferir a foto. Para recuperação, bloquear temporariamente , publicar, desbloquear e clicar em “Tentar finalizar novamente”; deve ocorrer nova confirmação sem novo envio ao storage. Também verificar legenda acima de 2.200 pontos de código.

A verificação ficou limitada ao componente isolado; lint, typecheck, build e infraestrutura real não foram executados conforme o escopo.
