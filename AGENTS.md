# Regras para Agentes

## Commit obrigatório

Ao finalizar qualquer alteração neste projeto, **sempre faça o commit** com o que foi feito.

### Formato do commit

Usar **Conventional Commits** em português:

```
<tipo>: <descrição curta>

<corpo com detalhes das mudanças em bullet points>
```

### Tipos

| Tipo | Quando usar |
|------|-------------|
| `feat` | Nova funcionalidade |
| `fix` | Correção de bug |
| `refactor` | Refatoração sem mudar comportamento |
| `docs` | Alteração em documentação |
| `chore` | Manutenção geral (deps, configs, etc.) |

### Exemplo

```
feat: adicionar flag --no-truncate para output completo

- Adicionada opção de linha de comando --no-truncate
- Quando ativa, desabilita todas as truncagens de conteúdo
- Atualizado README com documentação da nova flag
```

### Regras

1. Sempre fazer `git add` apenas dos arquivos modificados (não usar `git add .` cegamente).
2. A mensagem de commit deve descrever **o que foi feito e por quê**, não apenas "alterações".
3. Se houver múltiplas mudanças não relacionadas, fazer commits separados.
4. **Nunca** deixar alterações sem commit ao terminar uma tarefa.
