# Тема: Объединения.

## Запросы:

1. Вывести названия аудиторий, в которых читает лекции преподаватель “Edward Hopper”.

SELECT  LectureRooms.Name FROM Teachers INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId INNER JOIN Schedules ON Lectures.Id = Schedules.LectureId INNER JOIN LectureRooms ON Schedules.LectureRoomId = LectureRooms.Id WHERE Teachers.Name = "Edward" AND Teachers.Surname = "Hopper";

SELECT DISTINCT LectureRooms.Name FROM Teachers INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId INNER JOIN Schedules ON Lectures.Id = Schedules.LectureId INNER JOIN LectureRooms ON Schedules.LectureRoomId = LectureRooms.Id WHERE Teachers.Name = "Edward" AND Teachers.Surname = "Hopper"; - чтобы исключить повторы.

![текст](https://sun9-5.userapi.com/impg/88_h-aSUMgSTxPYB-UZg6EOhLoqH6V98_P8bdw/a86e2E7BfoQ.jpg?size=1920x1080&quality=95&sign=f9dca8d1c74e8cb33402fb8760b40657&type=album)

2. Вывести фамилии ассистентов, читающих лекции в группе “F505”.


![текст](url)

3. Вывести дисциплины, которые читает преподаватель “Alex Carmack” для групп 5-го курса.


![текст](url)

4. Вывести фамилии преподавателей, которые не читают лекции по понедельникам.


![текст](url)

5. Вывести названия аудиторий, с указанием их корпусов, в которых нет лекций в среду второй недели на третьей паре.


![текст](url)

6. Вывести полные имена преподавателей факультета “Computer Science”, которые не курируют группы кафедры “Software Development”.


![текст](url)

7. Вывести список номеров всех корпусов, которые имеются в таблицах факультетов, кафедр и аудиторий.


![текст](url)

8. Вывести полные имена преподавателей в следующем порядке: деканы факультетов, заведующие кафедрами, преподаватели, кураторы, ассистенты.


![текст](url)

9. Вывести дни недели (без повторений), в которые имеются занятия в аудиториях “A311” и “A104” корпуса 6.


![текст](url) 