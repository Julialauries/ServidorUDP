//Cliente:
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.util.Scanner;
public class ClienteUDP {
public static void main(String[] args) {
try {
DatagramSocket cliente = new DatagramSocket();
InetAddress enderecoServidor = InetAddress.getByName("localhost");
int portaServidor = 1478;
Scanner entrada = new Scanner(System.in);
while (true) {
// Lê mensagem do usuário
System.out.print("Digite uma mensagem para enviar para o servidor: ");
String mensagem = entrada.nextLine();
// Envia mensagem para o servidor
byte[] mensagemBytes = mensagem.getBytes();
DatagramPacket pacote = new DatagramPacket(mensagemBytes,
mensagemBytes.length, enderecoServidor, portaServidor);
cliente.send(pacote);
// Espera resposta do servidor
byte[] buffer = new byte[1024];
DatagramPacket pacoteResposta = new DatagramPacket(buffer,
buffer.length);
cliente.receive(pacoteResposta);
String resposta = new String(pacoteResposta.getData(), 0,
pacoteResposta.getLength());
System.out.println("Mensagem recebida do servidor: " + resposta);
}
} catch (IOException ex) {
System.out.println("Erro na criação do Cliente");
}
}
}
