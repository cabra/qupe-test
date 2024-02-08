# qupe-test


# 2.1 
Имеется база со следующими таблицами:

CREATE TABLE `users` (
  `id` INT(11) NOT NULL AUTO_INCREMENT, 
  `name` VARCHAR(255) DEFAULT NULL, 
  `gender` INT(11) NOT NULL COMMENT '0 - неуказан, 1 - мужчина, 2 - женщина.', 
  `birth_date` INT(11) NOT NULL COMMENT 'Дата в unixtime.', 
  PRIMARY KEY (`id`)
);
CREATE TABLE `phone_numbers` (
  `id` INT(11) NOT NULL AUTO_INCREMENT, 
  `user_id` INT(11) NOT NULL, 
  `phone` VARCHAR(255) DEFAULTNULL, 
  PRIMARYKEY (`id`)
);


Оптимизируйте структуру таблиц и напишите запрос, возвращающий имена и количества телефонных номеров девушек в возрасте от 18 до 30 лет.

# 2.2 
Проведите рефакторинг, исправьте баги и прокомментируйте код, приведённый ниже (таблица users здесь аналогична таблице users из предыдущей задачи)

    <?php
   function load_users_data($user_ids)
   {
       $user_ids = explode(",", $user_ids);
       foreach ($user_ids as $user_id) {
           $db = mysqli_connect("localhost", "root", "123123", "database");
           $sql = mysqli_query($db, "SEL ECT * FR OM users WHERE id=$user_id");
           while ($obj = $sql->fetch_object()) {
               $data[$user_id] = $obj->name;
           }
           mysqli_close($db);
       }
       return $data;
   }

   // Как правило, в $_GET['user_ids'] должна приходить строка с номерами пользователей через запятую, например: 1,2,17,48
   $data = load_users_data($_GET["user_ids"]);
   foreach ($data as $user_id => $name) {
       echo "<a href=\"/show_user.php?id=$user_id\">$name</a>";
   }

?>

Указать затраченное время
