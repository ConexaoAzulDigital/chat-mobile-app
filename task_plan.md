# Task Plan: Magica Chat — White-label Mobile App (Conexao Azul)

## Goal
Publicar o app Magica Chat (white-label do Chatwoot) nas lojas Play Store e App Store com branding Conexao Azul, URL padrão chat.conexaoazul.com e idioma pt_BR, validado primeiro em Android físico do dono.

## Current Phase
Phase 2 — Android Test Build

## Phases

### Phase 1: White-label & Branding (Fase 1)
- [x] Clonar repositório ConexaoAzulDigital/chat-mobile-app
- [x] Renomear app: Chatwoot → Magica Chat
- [x] Bundle ID: com.conexaoazul.magicachat (iOS e Android)
- [x] URL padrão: chat.conexaoazul.com
- [x] Locale padrão: pt_BR
- [x] Deep link scheme: magicachat://
- [x] Owner EAS: conexaoazul
- [x] Commit 82aff7e em branch develop
- **Status:** complete

### Phase 2: Android Test Build (dispositivo físico do Diego)
- [ ] Verificar pré-requisitos: pnpm, Android Studio, ADB ou EAS CLI
- [ ] Obter google-services.json (Firebase) OU desabilitar Firebase temporariamente para o build de teste
- [ ] Instalar dependências: pnpm install
- [ ] Build APK de desenvolvimento (EAS internal ou local)
- [ ] Instalar APK no Android via ADB
- [ ] Validar: tela inicial em PT-BR, URL pré-preenchida, login funcionando
- **Status:** in_progress

### Phase 3: Assets Visuais (Ícone, Splash, Adaptive Icon)
- [ ] Converter logo Conexao Azul Digital.png → ícone 1024x1024 PNG sem fundo
- [ ] Gerar adaptive-icon Android (foreground 108x108dp safe zone)
- [ ] Gerar splash screen 2048x2048 centralizado no logo
- [ ] Substituir assets/icon.png, assets/adaptive-icon.png, assets/splash.png
- [ ] Build com novos assets e validar visualmente
- **Status:** pending

### Phase 4: CI/CD GitHub Actions
- [ ] Criar .github/workflows/build-android.yml (EAS build on push)
- [ ] Criar .github/workflows/build-ios.yml
- [ ] Configurar GitHub Secrets: EAS token, Google Services, Apple certs
- [ ] Testar pipeline completo
- **Status:** pending

### Phase 5: Play Store — Publicação
- [ ] Criar conta Google Play Console (com.conexaoazul.magicachat)
- [ ] Gerar keystore Android assinado
- [ ] Build release AAB: eas build -p android --profile production
- [ ] Upload AAB para Play Console (internal testing primeiro)
- [ ] Preencher metadados PT-BR: título, descrição, screenshots
- [ ] Submeter para revisão
- **Status:** pending

### Phase 6: App Store — Publicação iOS
- [ ] Criar Apple Developer Account (suporte@conexaoazul.com)
- [ ] Configurar App ID: com.conexaoazul.magicachat
- [ ] Criar provisioning profile + certificate via EAS credentials
- [ ] Build release IPA: eas build -p ios --profile production
- [ ] Upload para App Store Connect
- [ ] Preencher metadados PT-BR
- [ ] Submeter para revisão
- **Status:** pending

### Phase 7: Skill magica-chat-ops
- [ ] Criar skill C:\Users\diego.vertrauen\.claude\skills\magica-chat-ops\
- [ ] Integrar EAS Build/Submit, versioning, notificações
- [ ] Documentar processo end-to-end
- **Status:** pending

## Key Questions
1. Diego tem Android Studio + ADB instalados no Windows? → A verificar
2. Tem google-services.json de projeto Firebase existente? → A verificar
3. Tem conta Expo (expo.dev)? → A criar com suporte@conexaoazul.com
4. Tem conta Google Play Console? → A verificar
5. Tem Apple Developer Account? → A verificar
6. Qual a cor HEX exata do azul do logo? → ~#2B3279 (pendente análise pixel)

## Decisions Made
| Decision | Rationale |
|----------|-----------|
| Caminho EAS Build (nuvem) para primeiro teste | Mais simples, sem precisar Android Studio completo |
| Desabilitar Firebase temporariamente para build de teste | Evita bloquear no google-services.json |
| Branch develop para todas as mudanças | Nunca commitar direto em main |
| Bundle ID com.conexaoazul.magicachat | Segue convenção reverse-domain da empresa |
| Locale padrão pt_BR (não pt) | Brasil é o mercado-alvo |

## Errors Encountered
| Error | Attempt | Resolution |
|-------|---------|------------|
| python3/python não disponível no PowerShell | 1 | Usado PowerShell nativo para tarefas de análise |
| git clone retornou exit code 1 | 1 | Era output do stderr do progresso — clone foi bem-sucedido |

## Notes
- Arquivos de planejamento ficam em: C:\Users\diego.vertrauen\Projects\chat-mobile-app\
- Repositório: https://github.com/ConexaoAzulDigital/chat-mobile-app
- Commit atual: 82aff7e (branch develop)
- Assets originais: C:\Users\diego.vertrauen\Pictures\Conexão Azul Digital.png (e .webp, mini.png)
