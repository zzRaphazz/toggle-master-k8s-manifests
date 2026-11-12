# Manifests Kubernetes — ToggleMaster

Este repositório é a fonte dos manifests Kubernetes gerenciados pelo Argo CD. Os diretórios de serviço em `apps/` usam Kustomize. Os recursos `Application` do Argo CD que apontam para cá ficam no repositório separado `toggle-master-argocd-config`.

## Importante antes do deploy

- O registry `000000000000` nas referências iniciais de imagem é um placeholder não funcional. Escolha e autorize a conta AWS, configure ECR/OIDC e permita que um pipeline aprovado publique e atualize cada imagem antes de iniciar os workloads.
- `platform/templates/` contém templates de configuração da Fase 2 ainda não referenciados pelas Applications do Argo CD. Não aplique esses arquivos diretamente: alguns têm placeholders Terraform não resolvidos, e o template de Secret nunca deve receber valores reais.
- Os workloads atuais referenciam ConfigMaps e Secrets de runtime. Defina uma forma segura de entrega de configuração/segredos antes de recriar ou fazer deploy no cluster.
- O workflow de CI atualiza somente a imagem selecionada neste repositório. Ele não executa `kubectl` nem faz deploy no cluster.
