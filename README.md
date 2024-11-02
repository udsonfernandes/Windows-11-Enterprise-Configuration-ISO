
# Windows 11 Enterprise Configuration ISO

Este repositório fornece instruções e scripts para configurar uma imagem ISO personalizada do Windows 11 com as configurações recomendadas para ambientes empresariais. Utilizamos as ferramentas GImageX e Dism++ para customizar a imagem, incluindo remoção de componentes desnecessários, otimizações de desempenho e configurações de segurança.

# Objetivo

O objetivo deste projeto é criar uma versão do Windows 11 ajustada para atender às necessidades de produtividade, segurança e eficiência de uma empresa (Fiz para atender uma empresa especifica, por isso não disponibilizarei a imagem ISO), facilitando a implantação do sistema em vários dispositivos.

# Ferramentas Utilizadas

# 1. [GImageX](https://www.autoitscript.com/site/autoit-tools/gimagex/)
   - Ferramenta GUI para a API ImageX que permite capturar, montar e aplicar imagens de disco WIM.
   - Utilizada para gerenciar e capturar imagens customizadas do Windows após a configuração.

# 2. [Dism++](https://www.chuyu.me/en/index.html)
   - Interface gráfica do DISM, permite a edição de imagens WIM com configurações adicionais.
   - Utilizada para otimizações, limpeza e remoção de componentes indesejados.

# Pré-requisitos

- Windows 10 ou 11 para rodar o processo de customização.
- Permissões de administrador para acessar e modificar imagens do sistema.
- As ferramentas [GImageX](https://www.autoitscript.com/site/autoit-tools/gimagex/) e [Dism++](https://www.chuyu.me/en/index.html) instaladas.

# Passo a Passo

# 1. Preparação do Ambiente

1. Baixe a ISO original do Windows 11 (edição apropriada) no [site oficial da Microsoft](https://www.microsoft.com/software-download/windows11).
2. Monte a ISO do Windows 11 ou extraia seu conteúdo para uma pasta temporária (exemplo: `C:\ISO_Windows11`).
3. Instale e abra as ferramentas GImageX e Dism++.

# 2. Montagem e Customização da Imagem

## Usando GImageX

1. Abra o GImageX e vá até a aba `Mount`.
2. No campo `Source`, selecione a imagem install.wim localizada em `C:\ISO_Windows11\sources`.
3. Escolha uma pasta de destino para montar a imagem (exemplo: `C:\MountedImage`).
4. Clique em `Mount` e aguarde até que a imagem esteja pronta para edição.

# Usando Dism++

1. Com a imagem montada, abra o Dism++.
2. Clique em `Open Session` e selecione a pasta onde a imagem foi montada (`C:\MountedImage`).
3. Utilize as ferramentas do Dism++ para aplicar as seguintes customizações:
   - Remoção de Aplicativos: Remova aplicativos não essenciais para o ambiente empresarial.
   - Configurações de Desempenho: Ajuste para desativar animações e otimizar o tempo de resposta.
   - Segurança: Ative configurações de segurança recomendadas (como desativar Telemetria e Cortana).
4. Salve as mudanças ao concluir as customizações.

# 3. Capturando e Salvando a Imagem

1. No GImageX, vá para a aba `Capture`.
2. Selecione o diretório de origem (`C:\MountedImage`) e o diretório de destino para salvar a nova imagem WIM customizada (exemplo: `C:\ISO_Custom\install.wim`).
3. Clique em `Capture` e aguarde a finalização do processo.

# 4. Criação da ISO Customizada

1. Substitua o arquivo `install.wim` original na pasta `C:\ISO_Windows11\sources` com o arquivo `install.wim` customizado.
2. Utilize uma ferramenta como o [OSCDIMG](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/oscdimg-command-line-options) para recriar a ISO:
   ```bash
   oscdimg -m -o -u2 -udfver102 -lWIN11_CUSTOM C:\ISO_Windows11 C:\ISO_Custom\Windows11_Custom.iso
   ```

# Testes

Antes de implantar a ISO em produção, recomendamos que:
1. Teste a instalação em um ambiente de sandbox ou VM.
2. Valide que as customizações e configurações estejam corretamente aplicadas.

# Avisos

- Modificar imagens do sistema pode afetar o suporte da Microsoft.
- Teste a ISO customizada antes de implementá-la em ambientes de produção.

# Contribuição

Contribuições são bem-vindas! Para colaborar:
1. Faça um fork deste repositório.
2. Crie uma nova branch para a sua feature.
3. Envie uma Pull Request com uma descrição detalhada das mudanças propostas.

---

Este README orienta o uso de GImageX e Dism++ para criar uma ISO do Windows 11 adaptada ao ambiente empresarial, mantendo uma estrutura clara para o uso no GitHub e facilitando a contribuição.
