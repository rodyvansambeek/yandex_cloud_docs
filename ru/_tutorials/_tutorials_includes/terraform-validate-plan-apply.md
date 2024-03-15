1. В терминале перейдите в папку, где вы отредактировали конфигурационный файл.
1. Проверьте корректность конфигурационного файла с помощью команды:

   ```bash
   terraform validate
   ```

   Если конфигурация является корректной, появится сообщение:

   ```bash
   Success! The configuration is valid.
   ```

1. Выполните команду:

   ```bash
   terraform plan
   ```

   В терминале будет выведен список ресурсов с параметрами. На этом этапе изменения не будут внесены. Если в конфигурации есть ошибки, {{ TF }} на них укажет.
1. Примените изменения конфигурации:

   ```bash
   terraform apply
   ```

1. Подтвердите изменения: введите в терминале слово `yes` и нажмите **Enter**.