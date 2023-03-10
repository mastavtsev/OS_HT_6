# OS_HT_6

В структуре сообщения message_t:
  server_pid - идентификатор процесса сервера, он записывается при запуске процесса сервера
  client_pid - идентификатор процесса клиента, он записывается при запуске процесса клиента
  random_num - случайно сгенерированное число
  type - тип сообщения 
  
  Запуск генерации клиентом происхоодит после ввода в консоль любой строки msg (len(msg) <= MAX_STRING - максимальная длина текстового сообщения), кроме "stop".
  
  Остановка программы возможно двумя способами: 
    1. Ввода в консоль у клиента строки "stop", после этого в msg_p->type в коде клиента будет записано значение msg_p->type = MSG_TYPE_FINISH. 
       Также в коде клиента произайдёт отсоедининение сегмента разделяемой памяти. Значение msg_p->type == MSG_TYPE_FINISH приведёт к msg_p->type = MSG_TYPE_EMPTY в коде
       сервера, что завершит его цикл while, после чего произойдёт удаление сегмента памяти.
    2. По нажатию CTRL + C в одной из программ. Для этого существует специальная функция обработчик sigfunc(int sig), которая обработает сигнал SIGINT в программе и
       и отправит сигнал SIGTERM в другую прогрмму. Процесс отсоединения и удаление сегмента памяти аналогичен пункту 1, то есть удаление происходит только в коде сервера.
