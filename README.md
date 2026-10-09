# Controley · versões para Android

Este repositório guarda só os instaladores do Controley (APK) e o arquivo `update.json` que o app consulta para saber se há versão nova.

O Controley é um controle remoto para TVs LG webOS pela rede Wi-Fi. O código do app não fica aqui.

## Instalar

Baixe o `controley.apk` da versão mais recente em **Releases** e abra no celular Android. Se o Android pedir, permita instalar apps desta origem.

Quem já tem o Controley 0.5.0 ou mais novo recebe as próximas versões pelo próprio app: um aviso aparece na aba Controle, e a nova versão instala por cima, mantendo o pareamento com a TV.

## Como o app procura atualização

Ao abrir (e ao voltar para o app, no máximo a cada 30 minutos) o Controley lê:

`https://raw.githubusercontent.com/diegocruzd3/controley-releases/main/update.json`

```json
{
  "versionCode": 7,
  "versionName": "0.5.0",
  "apkUrl": "https://github.com/diegocruzd3/controley-releases/releases/download/v0.5.0/controley.apk",
  "notes": "Texto curto mostrado no aviso."
}
```

O app só oferece a versão se `versionCode` for maior que o instalado, só baixa APK deste repositório e confere, antes de abrir o instalador, se o arquivo baixado é mesmo o Controley com esse `versionCode`.

## Publicar uma versão nova

1. Aumente `versionCode` (sempre um número maior) e `versionName` no projeto e assine com **a mesma chave** de sempre. Com outra chave o Android recusa instalar por cima.
2. Crie uma Release com a tag `vX.Y.Z` e anexe o APK com o nome `controley.apk`.
3. Só depois atualize o `update.json` aqui na branch `main` com o novo `versionCode`, `versionName`, `apkUrl` e `notes`.
