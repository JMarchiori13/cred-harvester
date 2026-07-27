# Contribuindo

Contribuições são bem-vindas **dentro do escopo do projeto**: pesquisa de credential access documentada, PoCs de laboratório e correções nas notas técnicas.

## Regras

1. **Somente material de laboratório.** Nada de credenciais reais, dumps de sistemas de produção ou dados de terceiros — nem anonimizados.
2. **Toda PoC precisa de doc.** Cada implementação em `src/` deve vir acompanhada de nota em `docs/` explicando a técnica, pré-requisitos e comportamento esperado.
3. **Sem código pronto para operação ofensiva.** PoCs devem ser didáticas: logging verboso, artefatos visíveis, sem ofuscação ou evasão de AV.
4. **Não commite artefatos sensíveis.** O `.gitignore` já cobre dumps, tíquetes e chaves — respeite-o.

## Processo

1. Abra uma issue descrevendo a técnica/módulo
2. Fork → branch `feat/<modulo>-<tecnica>`
3. PR com referência à issue e resultado do experimento de lab

## Padrões

- Notas em português ou inglês (mantenha consistência dentro do arquivo)
- Técnicas mapeadas para MITRE ATT&CK (técnica + sub-técnica)
- Tabelas para comparação de métodos
