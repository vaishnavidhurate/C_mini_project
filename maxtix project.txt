#include <stdio.h>

#define MAX 10

void inputMatrix(int matrix[MAX][MAX], int row, int col) {
    printf("Enter elements of the matrix (%dx%d):\n", row, col);
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }
}

void displayMatrix(int matrix[MAX][MAX], int row, int col) {
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
}

void addMatrices(int matrix1[MAX][MAX], int matrix2[MAX][MAX], int result[MAX][MAX], int row, int col) {
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            result[i][j] = matrix1[i][j] + matrix2[i][j];
        }
    }
}

void subtractMatrices(int matrix1[MAX][MAX], int matrix2[MAX][MAX], int result[MAX][MAX], int row, int col) {
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            result[i][j] = matrix1[i][j] - matrix2[i][j];
        }
    }
}

void multiplyMatrices(int matrix1[MAX][MAX], int matrix2[MAX][MAX], int result[MAX][MAX], int row1, int col1, int col2) {
    for (int i = 0; i < row1; i++) {
        for (int j = 0; j < col2; j++) {
            result[i][j] = 0;
            for (int k = 0; k < col1; k++) {
                result[i][j] += matrix1[i][k] * matrix2[k][j];
            }
        }
    }
}

int main() {
    int matrix1[MAX][MAX], matrix2[MAX][MAX], result[MAX][MAX];
    int row1, col1, row2, col2;
    int choice;

    printf("Enter rows and columns of first matrix: ");
    scanf("%d%d", &row1, &col1);

    inputMatrix(matrix1, row1, col1);

    printf("Enter rows and columns of second matrix: ");
    scanf("%d%d", &row2, &col2);

    inputMatrix(matrix2, row2, col2);

    printf("\nChoose the operation to perform:\n");
    printf("1. Addition\n");
    printf("2. Subtraction\n");
    printf("3. Multiplication\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            if (row1 == row2 && col1 == col2) {
                addMatrices(matrix1, matrix2, result, row1, col1);
                printf("Resultant Matrix after Addition:\n");
                displayMatrix(result, row1, col1);
            } else {
                printf("Matrices cannot be added, dimensions do not match.\n");
            }
            break;
        case 2:
            if (row1 == row2 && col1 == col2) {
                subtractMatrices(matrix1, matrix2, result, row1, col1);
                printf("Resultant Matrix after Subtraction:\n");
                displayMatrix(result, row1, col1);
            } else {
                printf("Matrices cannot be subtracted, dimensions do not match.\n");
            }
            break;
        case 3:
            if (col1 == row2) {
                multiplyMatrices(matrix1, matrix2, result, row1, col1, col2);
                printf("Resultant Matrix after Multiplication:\n");
                displayMatrix(result, row1, col2);
            } else {
                printf("Matrices cannot be multiplied, invalid dimensions.\n");
            }
            break;
        default:
            printf("Invalid choice.\n");
    }

    return 0;
}
