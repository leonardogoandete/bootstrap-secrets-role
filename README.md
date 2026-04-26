# bootstrap-secrets-template

Template de role Ansible para bootstrap de segredos via Bitwarden CLI.

## Como usar em outro repositorio

1. Copie o conteudo desta pasta para o novo repositorio.
2. Preencha os `bw_item_id` em `roles/bootstrap_secrets/defaults/main.yml`.
3. Execute com `BW_SESSION` ativo.

## Exemplo de itens

```yaml
bootstrap_secrets_items:
  - name: github_ssh_private_key
    bw_item_id: "UUID_DO_ITEM"
    dest: "{{ bootstrap_secrets_target_home }}/.ssh/id_ed25519"
    mode: "0600"
  - name: chezmoi_age_private_key
    bw_item_id: "UUID_DO_ITEM"
    dest: "{{ bootstrap_secrets_target_home }}/.config/chezmoi/age/key.txt"
    mode: "0600"
```

## Execucao

```bash
bw login
export BW_SESSION="$(bw unlock --raw)"
ansible-playbook -i inventory.ini playbook.yml -K
```

## Notas de seguranca

- Nunca suba chaves privadas no Git.
- Os segredos sao tratados com `no_log: true`.
- Prefira usar UUID dos itens no Bitwarden.
