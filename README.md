<img src="https://user-images.githubusercontent.com/2246121/282256557-1570674b-d142-4198-9740-69404cc6a339.png#gh-light-mode-only" width="100%" alt="Chat dashboard dark mode"/>
<img src="https://user-images.githubusercontent.com/2246121/282256632-87f6a01b-6467-4e0e-8a93-7bbf66d03a17.png#gh-dark-mode-only" width="100%" alt="Chat dashboard"/>

---

# Chatwoot

Mobile app for chatwoot platform. Built with React Native and Expo.

<p>
   <a href="https://github.com/react-native-community/releases/blob/master/CHANGELOG.md"><img src="https://img.shields.io/github/package-json/dependency-version/chatwoot/chatwoot-mobile-app/react-native?color=%2361dafb" alt="Project Dependencies"></a>
   <img src="https://img.shields.io/github/package-json/dependency-version/chatwoot/chatwoot-mobile-app/expo?color=%2361dafb" alt="Expo">
  <img src="https://img.shields.io/discord/647412545203994635" alt="Discord">
  <a href="https://discord.gg/cJXdrwS"><img src="https://img.shields.io/badge/chat-Discord-violet?logo=discord" alt="Chat on Discord"></a>
   <a href="http://makeapullrequest.com"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="Chat on Discord"></a>
 <img src="https://img.shields.io/github/license/chatwoot/chatwoot-mobile-app" alt="License">
</p>

- **Supported Chatwoot version:** 3.13.0+
- **Supported iOS versions**: 13.4+
- **Supported Android versions**: 6.0+

## Features

- Do not miss out on the new customers
- Follow up on customer conversations on go
- Reply easily with canned responses
- Receive realtime notifications about system activities
- Communicate with other team members via private notes
- Assign statuses to your conversations
  ... and more to come!

## Download Android/iOS application

<p >
  <a href="https://apps.apple.com/app/id1495796682">
    <img alt="Download on the App Store" title="App Store" src="http://i.imgur.com/0n2zqHD.png" width="140">
  </a>

  <a href="https://play.google.com/store/apps/details?id=com.chatwoot.app&hl=en">
    <img alt="Get it on Google Play" title="Google Play" src="http://i.imgur.com/mtGRPuM.png" width="140">
  </a>
</p>

## Testing

To help with testing app updates before they're released, you can:

Sign up to be a beta tester

- [Android](https://play.google.com/apps/testing/com.chatwoot.app) - Open this link from your Android device
- [iOS](https://testflight.apple.com/join/yQ4yoSx4) - Open this link from your iOS device

You can leave the Beta testing program at any time:

- On Android, [click this link](https://play.google.com/apps/testing/com.chatwoot.app) while logged in with your Google Play email address used to opt-in for the Beta program, then click **Leave the program**.
- On iOS, access the `Chatwoot` app page in TestFlight and click **Stop Testing**.

## Feedback & Contributing

Feel free to send us feedback on [X](https://x.com/chatwootapp) or [file an issue](https://github.com/chatwoot/chatwoot-mobile-app/issues).

If you wish to contribute, please take a quick look at the [CONTRIBUTING.md](https://www.chatwoot.com/docs/contributing-guide/mobile-app/setup-guide).

If there's anything you'd like to chat about, please feel free to join our [Discord](https://discord.gg/cJXdrwS) chat!

_Chatwoot_ &copy; 2017-2025, Chatwoot Inc - Released under the MIT License.

---

## CI/CD — Magica Chat (white-label)

### Workflows

| Workflow | Trigger | Jobs |
|---|---|---|
| `eas-build-android.yml` | PR para `main` | lint + build preview APK |
| `eas-build-android.yml` | push para `main` | build production AAB |
| `eas-build-ios.yml` | push para `main` | build production IPA |

### Build Profiles

| Profile | Platform | Distribuicao | Uso |
|---|---|---|---|
| `preview` | Android | Internal (APK) | Testes em PRs |
| `production` | Android + iOS | Store (AAB/IPA) | Release |
| `development` | Android + iOS | Internal | Dev client local |

### Configurar secrets no GitHub

Va em **Settings > Secrets and variables > Actions** no repositorio e adicione:

| Secret | Descricao | Como obter |
|---|---|---|
| `EXPO_TOKEN` | Token de autenticacao EAS | `npx expo login` → `~/.expo/state.json` ou [expo.dev/accounts](https://expo.dev/accounts) > Access Tokens |
| `GOOGLE_SERVICES_JSON` | `google-services.json` em base64 | `base64 -w 0 google-services.json` |
| `GOOGLE_SERVICES_PLIST` | `GoogleService-Info.plist` em base64 | `base64 -w 0 GoogleService-Info.plist` |
| `EXPO_APPLE_ID` | Apple ID (email) para autenticacao | Ex: `developer@conexaoazul.com` |
| `EXPO_APPLE_TEAM_ID` | Team ID da Apple Developer | [developer.apple.com](https://developer.apple.com/account) > Membership |

Codificar arquivos Firebase em base64 (Linux/macOS):

```bash
# Android
base64 -w 0 google-services.json | pbcopy

# iOS
base64 -w 0 GoogleService-Info.plist | pbcopy
```

No Windows (PowerShell):

```powershell
# Android
[Convert]::ToBase64String([IO.File]::ReadAllBytes("google-services.json")) | Set-Clipboard

# iOS
[Convert]::ToBase64String([IO.File]::ReadAllBytes("GoogleService-Info.plist")) | Set-Clipboard
```

### Como fazer um release

1. Desenvolva na branch `develop`
2. Abra um PR de `develop` para `main`
   - O workflow dispara `lint` + `build-preview` (APK para testes)
3. Aprove e mergue o PR
   - O workflow dispara `build-production` (Android AAB + iOS IPA via EAS)
4. Acompanhe os builds em [expo.dev/accounts/conexao-azul/projects/magica-chat](https://expo.dev/accounts/conexao-azul/projects/magica-chat)
5. Submeta para as stores quando o build EAS estiver pronto:
   ```bash
   pnpm submit:android   # Google Play (track: internal)
   pnpm submit:ios       # App Store Connect
   ```

### EAS Project

- **Conta:** `conexao-azul`
- **Projeto:** `magica-chat`
- **Project ID:** `2a9ff588-2989-4260-b49a-0ddc8c493ab1`
- **Bundle ID Android:** `com.conexaoazul.magicachat`
- **Bundle ID iOS:** `com.conexaoazul.magicachat`
