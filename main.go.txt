package main
import "fmt"


type Aluno struct {
  Id int
  Nome string
  Nota int
}

func showMenu() {
  fmt.Println("\nMenu: \n(1) Adicionar Aluno\n(2) Consultar Aluno\n(3) Deletar Aluno\n(4) Atualizar Aluno");
}

func chooseOption() int{
  var option int;
  fmt.Print("\nDigite sua opção: ");
  fmt.Scan(&option);

  return option;
}

func adicionarAluno() Aluno {

  var id int;
  fmt.Print("\nDigite o id do aluno: ");
  fmt.Scan(&id);

  var nome string;
  fmt.Print("Digite o nome do aluno: ");
  fmt.Scan(&nome);

  var nota int;
  fmt.Print("Digite a nota do aluno: ");
  fmt.Scan(&nota);
  
  a := Aluno{
    Id: id,
    Nome: nome,
    Nota: nota,
  }

  return a;
}

func consultarAluno(alunos []Aluno){
    var id int;
    get := 0;
        fmt.Print("\nDigite o Id do aluno que quer consultar: ");
        fmt.Scan(&id);
        
        for i := 0; i < len(alunos); i++{
          if alunos[i].Id == id {
            get = 1;
            
            fmt.Println("\nNome do aluno:", alunos[i].Nome);
            fmt.Println("Nota do aluno:", alunos[i].Nota);
          }
        }
  if get == 0{
    fmt.Println("Aluno não encontrado!");
  }
}

func deletarAluno(alunos []Aluno) []Aluno{
  alunosCopy := []Aluno{};
  var id int;
  get := 0;
  
  fmt.Print("\nDigite o Id do aluno que quer remover: ");
  fmt.Scan(&id);
  for i := 0; i < len(alunos); i++{
    if alunos[i].Id == id{
      get = 1;
      continue;
    }
    alunosCopy = append(alunosCopy, alunos[i]);
  }

  if get == 0{
    fmt.Println("Aluno não encontrado!");
  } else{
    fmt.Println("Aluno deletado!");
  }

  return alunosCopy;
  
}

func atualizarAluno(alunos []Aluno){
  var id int;
  fmt.Print("\nDigite o id do aluno que quer atualizar: ");
  fmt.Scan(&id);

  get := 0;

  for i := 0; i < len(alunos); i++{
    if alunos[i].Id == id{
      get = 1;
      var nome string;
      var nota int;

      fmt.Print("Digite o novo nome: ");
      fmt.Scan(&nome);
      fmt.Print("Digite a nova nota: ");
      fmt.Scan(&nota);
      fmt.Println("Aluno atualizado!");

      alunos[i].Nome = nome;
      alunos[i].Nota = nota;
      
    }
  }

  if get == 0{
    fmt.Println("Aluno não encontrado!");
  }
}

func main() {

  alunos := []Aluno{}
  
    for true{
      showMenu()
      option := chooseOption();
    
      if option == 1 {
        aluno := adicionarAluno()
        sameId := 0;
        for i := 0; i < len(alunos); i++{
          if alunos[i].Id == aluno.Id{
            sameId = 1;
          }
        }
        if sameId == 0{
          alunos = append(alunos, aluno)
        } else{
          fmt.Println("Falha! Já existe um aluno cadastrado com esse Id!")
        }
        
      } else if option == 2{
        consultarAluno(alunos);
        
      } else if option == 3{
        alunos = deletarAluno(alunos);
        
      } else if option == 4{
        atualizarAluno(alunos);
        
      }


  }

    
}
