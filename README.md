<a href="https://laravel.com"> <img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125950651155881984/1200px-Laravel.svg_preview_rev_1.png" width=260 height=200></a> <a href="https://www.php.net"> <img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125951200420970547/download_preview_rev_1_1.png" width=250 height=200></a> <a href="https://code.visualstudio.com"> <img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125953674926112778/channels4_profile_preview_rev_1.png" align=left width=250 height=200></a> 

<h1>Trabalho da matéria de Criação de API Rest básica com PHP</h1>

<h1>Professor João Vitor da Costa Andrade</h1>

Aplicação de API Rest Usando PHP em banco de dados MySQL. Sistemas de gerenciamento de tarefas utilizando laravel. O sistema é capaz de:

- Listar todas as tarefas.
- Dar detalhes sobre uma tarefa específica.
- Adicionar uma nova tarefa.
- Atualizar os dados da tarefa.
- Excluir alguma tarefa.

<h1>Instruções de como fazer o Sistema</h1>

- Abra o git bash e de um "git clone" do URL do repositório do projeto-laravel do Professor João.
- Após isso de um "cd projeto-laravel/" para poder entrar na pasta
- Ainda no git bash de o comando "code .". para acessar o vs code do projeto-laravel.
Após abrir o vs code, digite os seguintes códigos:
- Na pasta app/Http/Controllers/TaskController.php:
````php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Task;

class TaskController extends Controller
{
   public function index()
   {
       $tasks = Task::all();

       return response()->json($tasks);
   }

   public function show($id)
   {
       $task = Task::find($id);

       if ($task) {
           return response()->json($task);
       } else {
           return response()->json(['error' => 'Tarefa não encontrada'], 404);
       }
   }

   public function store(Request $request)
   {
       $request->validate([
           'title' => 'required',
           'description' => 'required',
       ]);

       $task = new Task;
       $task->title = $request->input('title');
       $task->description = $request->input('description');
       $task->status = $request->input('status', false);
       $task->save();

       return response()->json($task, 201);
   }

   public function update(Request $request, $id)
   {
       $task = Task::find($id);

       if ($task) {
           $request->validate([
               'title' => 'required',
               'description' => 'required',
           ]);

           $task->title = $request->input('title');
           $task->description = $request->input('description');
           $task->status = $request->input('status', $task->status);
           $task->save();

           return response()->json($task);
       } else {
           return response()->json(['error' => 'Tarefa não encontrada'], 404);
       }
   }

   public function destroy($id)
   {
       $task = Task::find($id);

       if ($task) {
           $task->delete();

           return response()->json(['message' => 'Tarefa excluída com sucesso']);
       } else {
           return response()->json(['error' => 'Tarefa não encontrada'], 404);
       }
   }
}
````
- Na pasta database/migrations/2023_06_27_221132_create_tasks_table.php
````php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTasksTable extends Migration
{
   public function up()
   {
       Schema::create('tasks', function (Blueprint $table) {
           $table->id();
           $table->string('title');
           $table->text('description');
           $table->boolean('status')->default(false);
           $table->timestamps();
       });
   }

   public function down()
   {
       Schema::dropIfExists('tasks');
   }
}
````
- Na pasta routes/api.php:
````php
<?php

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;

Route::get('/tasks', 'TaskController@index');
Route::get('/tasks/{id}', 'TaskController@show');
Route::post('/tasks', 'TaskController@store');
Route::put('/tasks/{id}', 'TaskController@update');
Route::delete('/tasks/{id}', 'TaskController@destroy');
````
- Na pasta routes/web.php:
````php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\TaskController;

Route::get('/tasks', [TaskController::class, 'index']);
Route::get('/tasks/{id}', [TaskController::class, 'show']);
Route::post('/tasks', [TaskController::class, 'store']);
Route::put('/tasks/{id}', [TaskController::class, 'update']);
Route::delete('/tasks/{id}', [TaskController::class, 'destroy']);
````

- Após isso copie e cole o ".env.example" novamente e renomeie apenas para ".env"
- Abra o terminal apertando "CTRL+' " e insira "composer install" para poder baixar as dependências do projeto
- Inicie no XAMPP e de start no Apache e MySQL.
- Ainda no terminal insire "php artisan migrate" e "php artisan serve" para poder iniciar o server.
- Depois disso é abrir o Postman e criar uma new collection e add resquest para poder criar as funções
- Após isso é só criar as tarefas do jeito desejado.
  
<h1>Clique na imagem do youtube, ou no link para ter acesso ao vídeo:</h1>

https://youtu.be/iBC8yvl9X90

<a href="https://youtu.be/iBC8yvl9X90"> <img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125959772022255657/yt_1200_preview_rev_1.png" align=left width=300 height=200></a> 


