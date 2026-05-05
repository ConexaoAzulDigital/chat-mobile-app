# Findings & Decisions — Magica Chat

## Requirements
- White-label do Chatwoot (React Native + Expo) como "Magica Chat"
- Empresa: Conexao Azul Digital (www.conexaoazul.com)
- URL de produção: https://chat.conexaoazul.com
- Idioma padrão: pt_BR (Português Brasil)
- Publicar: Play Store + App Store
- Validar primeiro em Android físico do Diego
- Usar multi-agente para velocidade e eficiência

## Research Findings

### Stack do Repositório
- React Native 0.76.9 + Expo SDK 52
- EAS Build (Expo Application Services) para builds nativos
- TypeScript + Redux Toolkit + TailwindCSS (twrnc)
- Firebase (push notifications): @react-native-firebase/app + messaging
- Sentry para error tracking
- pnpm 10.11.0 como package manager
- i18n-js com 30+ idiomas incluindo pt_BR pronto
- Notifee para notificações locais (requer Google Services)

### Arquivos Críticos para White-label
| Arquivo | Mudança Aplicada |
|---------|-----------------|
| app.config.ts | name, slug, scheme, bundleIdentifier, package, host, owner |
| settingsSlice.ts | baseUrl, installationUrl, webSocketUrl, localeValue |
| ConfigURLScreen.tsx | URL padrão do campo de input |
| i18n/index.js | locale padrão = pt_BR |
| constants/index.ts | SSO callback scheme |
| .env.example | URL base |
| package.json | nome do pacote |

### Dependências Nativas (bloqueiam Expo Go)
- @react-native-firebase/app e messaging → precisa google-services.json
- @notifee/react-native → push notifications nativas
- ffmpeg-kit-react-native → processamento de áudio/vídeo
- react-native-permissions → câmera, microfone, fotos

### MCPs Disponíveis e Utilidade
| MCP | Utilidade para este projeto |
|-----|----------------------------|
| GitHub MCP | Triggers CI/CD, releases, PRs |
| Google Drive MCP | Armazenar assets, screenshots de loja |
| N8N MCP | Automação de deploy/notificações pós-build |
| Google Workspace MCP | Notificações email de build status |

### Gaps Identificados
- Nenhum MCP nativo para EAS Build/Submit
- Nenhum MCP para Play Store / App Store APIs
- Nenhum .github/workflows ainda
- Keystore Android não configurado
- Apple Developer Account pendente
- google-services.json necessário para build completo

### Cor do Logo Conexao Azul
- Azul marinho escuro: ~#2B3279 (estimativa visual — logo é SVG/PNG navy)
- Fundo: branco (#ffffff)
- Confirmar pixel-exato quando Python disponível ou via editor gráfico

### EAS Build — Configuração Atual
```json
{
  "build": {
    "development": { "developmentClient": true, "distribution": "internal" },
    "production": { "autoIncrement": true }
  },
  "submit": {
    "production": { "android": { "track": "internal" } }
  }
}
```

## Technical Decisions
| Decision | Rationale |
|----------|-----------|
| EAS Build (nuvem) para primeiro teste Android | Sem necessidade de Android Studio completo |
| Desabilitar Firebase para build de teste inicial | Desbloqueia compilação sem google-services.json |
| Branch develop, nunca main | Segurança, PR flow como definido na arquitetura |
| pt_BR como locale padrão (i18n/index.js) | Tradução já existe no repositório |
| magicachat:// como URL scheme | Consistente com nome do app |

## Issues Encountered
| Issue | Resolution |
|-------|------------|
| python3 indisponível no PowerShell para análise de cor | Usar ferramenta gráfica ou editor de imagem |
| App usa módulos nativos pesados | Expo Go não funciona; precisa build nativo |

## Resources
- Repositório: https://github.com/ConexaoAzulDigital/chat-mobile-app
- EAS Build docs: https://docs.expo.dev/build/introduction/
- Firebase Console: https://console.firebase.google.com
- Play Console: https://play.google.com/console
- App Store Connect: https://appstoreconnect.apple.com
- Logo fonte: C:\Users\diego.vertrauen\Pictures\Conexão Azul Digital.png

## Visual/Browser Findings
- Logo Magica Chat: ícone estilizado em "X" ou letra hebraica, azul marinho escuro sobre fundo branco
- App terá fundo branco (#ffffff) no splash e adaptive-icon background
- Cor primária: navy blue ~#2B3279 (a confirmar)
