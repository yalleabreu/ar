# App Pesquisa de Campo - Android

Aplicativo Android nativo para coleta de dados em campo com funcionamento 100% offline.

## Requisitos

- **Android Studio** Arctic Fox ou superior
- **JDK 11** ou superior
- **Android SDK** 34 (pode ser instalado pelo Android Studio)
- **Gradle 8.0** (incluído no projeto)

## Como Compilar

### Opção 1: Android Studio (Recomendado)

1. Abra o Android Studio
2. Clique em **File > Open**
3. Selecione a pasta `android-app`
4. Aguarde o Gradle sincronizar (pode demorar alguns minutos)
5. Clique em **Build > Build Bundle(s) / APK(s) > Build APK(s)**
6. O APK será gerado em `app/build/outputs/apk/debug/app-debug.apk`

### Opção 2: Linha de Comando

```bash
cd android-app

# Linux/macOS
./gradlew assembleDebug

# Windows
gradlew.bat assembleDebug
```

O APK será gerado em `app/build/outputs/apk/debug/app-debug.apk`

### Gerar APK de Release (para distribuição)

```bash
# Gerar APK assinado para produção
./gradlew assembleRelease
```

**Nota**: Para release, você precisa configurar a assinatura em `app/build.gradle`.

## Instalação no Dispositivo

1. Copie o arquivo `app-debug.apk` para o dispositivo Android
2. No dispositivo, vá em **Configurações > Segurança > Fontes desconhecidas** (habilitar)
3. Abra o arquivo APK e instale

Ou via ADB:
```bash
adb install app/build/outputs/apk/debug/app-debug.apk
```

## Configuração do App

Após instalar:

1. Abra o app
2. Na primeira execução, configure:
   - **URL da API**: Endereço do servidor (ex: `https://seu-servidor.com`)
   - **Código da Pesquisa**: Código de 6 dígitos gerado no painel web
3. Clique em **Salvar**
4. O app baixará a pesquisa automaticamente

## Funcionalidades

- Funciona 100% offline
- Coleta localização GPS discretamente
- Grava áudio em segundo plano
- Armazena respostas localmente até envio manual
- Suporte a múltiplos tipos de perguntas
- Envio em lote quando online

## Estrutura do Projeto

```
android-app/
├── app/
│   ├── src/main/
│   │   ├── java/com/pesquisa/app/
│   │   │   ├── activities/      # Telas do app
│   │   │   ├── adapters/        # Adaptadores de lista
│   │   │   ├── api/             # Cliente Retrofit
│   │   │   ├── database/        # Room Database
│   │   │   ├── models/          # Modelos de dados
│   │   │   ├── services/        # Serviços em background
│   │   │   └── PesquisaApp.java # Application class
│   │   ├── res/
│   │   │   ├── layout/          # Layouts XML
│   │   │   ├── values/          # Strings, cores, temas
│   │   │   └── drawable/        # Ícones e imagens
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── build.gradle
├── settings.gradle
└── gradle.properties
```

## Permissões Necessárias

O app solicita as seguintes permissões:

- **Internet**: Para enviar dados ao servidor
- **Localização**: Para coletar coordenadas GPS
- **Microfone**: Para gravação de áudio
- **Localização em segundo plano**: Para rastreamento contínuo

## Troubleshooting

### Erro "SDK location not found"

Crie o arquivo `local.properties` na raiz do projeto:
```
sdk.dir=/caminho/para/android/sdk
```

### Erro de versão do Gradle

O projeto usa Gradle 8.0. Se tiver problemas, atualize o Android Studio.

### APK não instala

Verifique se "Fontes desconhecidas" está habilitado nas configurações do dispositivo.
