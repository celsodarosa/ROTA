[README.md](https://github.com/user-attachments/files/32861457/README.md)
# Rota — sugestões de lugares no trajeto (Android + iOS)

## Estrutura
```
rota-app/
├── App.js                    # Navegação (Login → Abas) + contexto de autenticação
├── app.json                  # Config Expo (coloque a chave do Google Maps)
├── package.json
└── src/
    ├── theme.js              # Paleta azul/branco, raios, sombras
    ├── storage.js            # Cadastro/login/histórico (AsyncStorage – MVP)
    ├── services/places.js    # Directions + Places API (sugestões ao longo da rota)
    └── screens/
        ├── LoginScreen.js    # Login/Cadastro
        ├── MapScreen.js      # Mapa, origem/destino, categorias, lista de sugestões
        └── HistoryScreen.js  # Histórico em lista
```

## Como rodar
1. `npm install`
2. No Google Cloud: ative **Maps SDK (Android/iOS), Directions API e Places API**, crie uma chave.
3. Substitua `SUA_CHAVE_AQUI` em `app.json` e `src/services/places.js`.
4. `npx expo start` → escaneie o QR code com o app Expo Go (Android/iOS).

## Como funciona
Rota (Directions) → amostra ~5 pontos do trajeto → busca lugares por categoria perto de cada ponto (Places) →
filtra nota ≥ 4,0 e ≥ 20 avaliações → ordena por nota. Cada busca é salva no histórico do usuário.

## Próximos passos recomendados
- Trocar `storage.js` por Firebase Auth + Firestore (senha hasheada, sincronização entre aparelhos).
- Mover chamadas às APIs do Google para um backend (proteger a chave).
- Autocomplete de endereços, favoritos, abrir rota no Google Maps/Waze, filtro "aberto agora".

## Validação com GitHub
```
git init && git add . && git commit -m "Rota: versão inicial"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/rota-app.git && git push -u origin main
```
- Cada push/PR roda **lint + testes + exportação Android** (aba *Actions*).
- Em `main`, o job `apk` gera um **APK de teste** (aba *Actions* → execução → *Artifacts* → `rota-debug-apk`).
- Chave do Google: *Settings → Secrets and variables → Actions → New secret* `GOOGLE_MAPS_API_KEY`.
- Local: `npm run validate`.
