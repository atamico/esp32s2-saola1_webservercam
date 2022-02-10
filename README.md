## USB Camera + Wi-Fi Transfer Example (EM DESENVOLVIMENTO)

Exemplo de transferência de câmera USB + Wi-Fi

Este exemplo implementa a leitura de fluxo MJPEG da câmera USB + transferência de imagem Wi-Fi por meio do Soc da série ESP32-S2 ou ESP32-S3 e oferece suporte às seguintes funções:

    Suporte para leitura e análise de fluxos de dados da câmera USB
    Suporte a configuração de Wi-Fi para o modo AP ou STA
    Suporte para transferência gráfica HTTP, você pode usar dispositivos móveis ou navegador de PC para visualizar as imagens ao vivo

Requisito de Hardware

Você pode usar qualquer placa de desenvolvimento ESP32-S2 ou ESP32-S3 integrada com PSRAM

    As câmeras que atendem aos seguintes parâmetros necessários são suportadas:
        Câmera compatível com o modo de velocidade total USB1.1
        A câmera vem com compressão MJPEG
        A câmera suporta a configuração da interface Max Packet Size para 512
        A largura de banda de transferência de imagem deve ser inferior a 4 Mbps, 
        pois usamos 512 Bytes de tamanho de pacote com transferência isócrona, apenas um pacote pode ser transmitido por milissegundo neste modo.
        Devido à limitação da largura de banda de transferência isócrona do USB, 
        a taxa de quadros da imagem e o tamanho da imagem única são mutuamente restritos.
        Se o tamanho da imagem for 25 KB por quadro, a taxa de quadros não pode ultrapassar 20 FPS
        Este exemplo oferece suporte a qualquer resolução que satisfaça as condições acima, pois nenhuma decodificação local é necessária

    Fiação do hardware da câmera USB.
        Por favor, use fonte de alimentação de 5V para a câmera USB VBUS, ou use IO para controlar VBUS ON/OFF.
        Linha de dados D + D- da câmera USB, siga o alinhamento padrão do sinal diferencial regular
        Câmera USB D+ (fio verde) para ESP32-S2/S3 GPIO20
        Câmera USB D- (fio branco) para ESP32-S2/S3 GPIO19

### Exemplo de compilação

O código de exemplo requer um PSRAM adicional de 2 MB e pode ser usado com placas de desenvolvimento como ESP32-S2-Saola-1 e ESP32-S2-Kaluga-1 baseadas no módulo ESP32-S2-WROVER.

1. Instalação do VStudio Code: 

        https://code.visualstudio.com/download
    
2. extenção PlatformIO

        Dentro do VS, Ctrl+Shift+X
        buscar e instalar PlatformIO IDE

    2.1. Instalação do "Espressif 32" dentro do PlatformIO

        Abrir PlatformIO;
        Abrir painel Platforms
        Buscar e instalar "Espressif 32"
    
 3.Compilação
 
        A compilação e uoload para o ESP pode ser feita pela barra de tarefas inferior.

### Como usar

Como usar

    Use o acesso de PC ou dispositivos móveis ao hotspot Wi-Fi do ESP32-S2/S3, SSID: ESP32S2-UVC Sem senha por padrão
    Digite 192.168.4.1 em seu navegador para abrir a janela de operação
    Clique em Iniciar transmissão para iniciar a transmissão de vídeo
    Clique em Parar para tirar uma foto
    Clique na janela de visualização Salvar para salvar a imagem atual

Parâmetros de desempenho

Sob a limitação de largura de banda de transferência isócrona USB, 
a taxa de compressão de imagens de resolução diferente corresponde à taxa de quadros:

Taxa de transferência de imagem de 320*240 até 33 quadros por segundo em uma taxa de compactação de 15:1, 
com um tamanho de imagem de aproximadamente 15 KB por quadro:

Taxas de taxa de transferência de imagem de 640*480 até 15 quadros por segundo em uma taxa de compactação de 25:1, 
com um tamanho de imagem de aproximadamente 36 KB por quadro: 
