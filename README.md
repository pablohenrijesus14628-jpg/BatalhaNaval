import java.util.Random;
import java.util.Scanner;

public class BatalhaNaval {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Random random = new Random();

        int tamanho = 5;
        char[][] tabuleiro = new char[tamanho][tamanho];

        // Inicializa o tabuleiro com água
        for (int i = 0; i < tamanho; i++) {
            for (int j = 0; j < tamanho; j++) {
                tabuleiro[i][j] = '~';
            }
        }

        // Coloca um navio de tamanho 3 horizontalmente
        int linhaNavio = random.nextInt(tamanho);
        int colunaNavio = random.nextInt(tamanho - 2);

        boolean[][] navio = new boolean[tamanho][tamanho];
        for (int i = 0; i < 3; i++) {
            navio[linhaNavio][colunaNavio + i] = true;
        }

        int acertos = 0;

        System.out.println("=== BATALHA NAVAL ===");

        while (acertos < 3) {
            imprimirTabuleiro(tabuleiro);

            System.out.print("Digite a linha (0 a 4): ");
            int linha = sc.nextInt();

            System.out.print("Digite a coluna (0 a 4): ");
            int coluna = sc.nextInt();

            if (linha < 0 || linha >= tamanho || coluna < 0 || coluna >= tamanho) {
                System.out.println("Posição inválida.");
                continue;
            }

            if (tabuleiro[linha][coluna] != '~') {
                System.out.println("Você já tentou essa posição.");
                continue;
            }

            if (navio[linha][coluna]) {
                System.out.println("Acertou!");
                tabuleiro[linha][coluna] = 'X';
                acertos++;
            } else {
                System.out.println("Água!");
                tabuleiro[linha][coluna] = 'O';
            }
        }

        System.out.println("Parabéns! Você afundou o navio!");
        imprimirTabuleiro(tabuleiro);

        sc.close();
    }

    static void imprimirTabuleiro(char[][] tabuleiro) {
        System.out.println();
        for (int i = 0; i < tabuleiro.length; i++) {
            for (int j = 0; j < tabuleiro[i].length; j++) {
                System.out.print(tabuleiro[i][j] + " ");
            }
            System.out.println();
        }
        System.out.println();
    }
}

