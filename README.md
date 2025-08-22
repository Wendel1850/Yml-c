#include <sqlite3.h>
#include <stdio.h>

int main() {
    sqlite3 *db;
    char *errMsg;

    // Abrir o banco de dados
    int rc = sqlite3_open("banco.db", &db);
    if (rc) {
        fprintf(stderr, "Não foi possível abrir o banco de dados: %s\n", sqlite3_errmsg(db));
        return 1;
    }

    // Executar uma query
    const char *sql = "SELECT * FROM tabela";
    rc = sqlite3_exec(db, sql, NULL, NULL, &errMsg);
    if (rc != SQLITE_OK) {
        fprintf(stderr, "Erro ao executar a query: %s\n", errMsg);
        sqlite3_free(errMsg);
    }

    // Fechar o banco de dados
    sqlite3_close(db);
    return 0;
}
