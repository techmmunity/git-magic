# Gitflow

## Sumário

- [Branches](#branches)
- [Como criar uma nova feature?](#como-criar-uma-nova-feature)
- [Eu esqueci de criar uma branch antes de desenvolver a feature, isso é um problema?](#eu-esqueci-de-criar-uma-branch-antes-de-desenvolver-a-feature-isso-%C3%A9-um-problema)
- [Como criar uma nova feature enquanto uma outra que eu dependo ainda nao foi mergeada?](#como-criar-uma-nova-feature-enquanto-uma-outra-que-eu-dependo-ainda-nao-foi-mergeada)

## Branches

| branch      | descrição                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------ |
| `master`    | Branch mais atualizada (branch de desenvolvimento)                                               |
| `feature/*` | Branches onde algo que modifique o funcionamento do software será adicionado ou alterado         |
| `fix/*`     | Branches para correção de bugs                                                                   |
| `chore/*`   | Branches para atualizar documentacoes, CI/CD e coisas que nao afetem o funcionamento do software |
| `version/*` | Branches para atualizar a versão do software                                                     |

## Como criar uma nova feature?

```yml
[master]              $ git pl # Para fazer o pull das mudanças mais recentes da master
[master]              $ git cb feature/new-feature # Para criar uma nova branch
[feature/new-feature] # Faça a nova feature
[feature/new-feature] $ git acips Commit Message # To add, commit and push the changes
[GitHub]              # Crie um PR
[GitHub]              # Faça o merge do PR (de preferência usando SQUASH)
[feature/new-feature] $ git ckm # Para voltar para a master e fazer o pull das mudanças mais recentes
[master]              $ git bd feature/new-feature # Para deletar a branch feature/new-feature
[master]              $ git gone # Para deletar completamente a branch feature/new-feature
[master]              # Faça isso de novo e de novo :)
```

## Eu esqueci de criar uma branch antes de desenvolver a feature, isso é um problema?

Nãp! Isso não é um problema, mas lembre-se, **isso é uma pessima pratica**, então tente não fazer isso novamente, ok? Ou alguma hora isso vai te causar problemas terriveis!

Para resolver isso, basta executar os seguintes comandos:

```yml
[master]              # Com as mudanças da sua feature
[master]              $ git cb feature/new-feature # Para criar uma nova branch
[feature/new-feature] # Continue com o de sempre :)
```

## Como criar uma nova feature enquanto uma outra que eu dependo ainda nao foi mergeada?

**Alert:** Fazer features que dependendem de outras é uma coisa muito perigosa. Sempre tente evitar fazer isso.

```yml
[feature/feature-one]     # Logo depois de usar `acips` e criar o PR!!!
[feature/feature-one]     $ git cb feature/another-feature # Para criar uma nova branch
[feature/another-feature] # Faça a nova feature
[feature/another-feature] $ git acips Commit Message # Para fazer o add, commit e push das mudanças
[GitHub]                  # Faça o merge do PR da branch feature/feature-one
[feature/another-feature] $ git ckm # Para voltar para a master e fazer o pull das mudanças
[master]                  $ git ck feature/another-feature # Para voltar para a feature/another-feature
[feature/another-feature] $ git rbm # Para aplicar as mudanças da master na sua branch
[feature/another-feature] $ git ps # Para enviar sua branch atualizada para o GitHub
[GitHub]                  # Crie o novo PR
[GitHub]                  # Faça o merge desse PR (de preferência usando SQUASH)
[feature/another-feature] $ git ckm # Para voltar para a master e fazer o pull das mudanças mais recentes
[master]                  $ git bd feature/feature-one # Para deletar a feature/feature-one branch
[master]                  $ git bd feature/another-feature # Para deletar a feature/another-feature branch
[master]                  $ git gone # Para remover completamente ambas as branches
[master]                  # Faça isso de novo e de novo :)
```
