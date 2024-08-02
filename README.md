# Тема: Объединения.

## Запросы:

1. Вывести названия аудиторий, в которых читает лекции преподаватель “Edward Hopper”.

SELECT  LectureRooms.Name FROM Teachers INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId INNER JOIN Schedules ON Lectures.Id = Schedules.LectureId INNER JOIN LectureRooms ON Schedules.LectureRoomId = LectureRooms.Id WHERE Teachers.Name = "Edward" AND Teachers.Surname = "Hopper";

SELECT DISTINCT LectureRooms.Name FROM Teachers INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId INNER JOIN Schedules ON Lectures.Id = Schedules.LectureId INNER JOIN LectureRooms ON Schedules.LectureRoomId = LectureRooms.Id WHERE Teachers.Name = "Edward" AND Teachers.Surname = "Hopper"; - чтобы исключить повторы.

![текст](https://sun9-5.userapi.com/impg/88_h-aSUMgSTxPYB-UZg6EOhLoqH6V98_P8bdw/a86e2E7BfoQ.jpg?size=1920x1080&quality=95&sign=f9dca8d1c74e8cb33402fb8760b40657&type=album)

2. Вывести фамилии ассистентов, читающих лекции в группе “F505”.

SELECT Surname FROM Assistants, Teachers, Lectures, GroupsLectures, `Groups` WHERE Assistants.TeacherId=Teachers.Id AND Teachers.Id = Lectures.TeacherId AND Lectures.Id = GroupsLectures.LectureId AND GroupsLectures.GroupId = `Groups`.Id AND `Groups`.Name = "F505";

SELECT Surname FROM Teachers INNER JOIN Assistants ON Teachers.Id = Assistants.TeacherId INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId INNER JOIN GroupsLectures ON Lectures.Id = GroupsLectures.LectureId INNER JOIN `Groups` ON GroupsLectures.GroupId = `Groups`.Id WHERE `Groups`.Name = "F505";

![текст](https://sun9-20.userapi.com/impg/xOduMdsbolY0PSm0iz_C9QFbK8Vdcjo4yJo_iQ/83is2vfZiZ0.jpg?size=1920x1080&quality=95&sign=fe6adcda5a544105a6c436f124056664&type=album)

3. Вывести дисциплины, которые читает преподаватель “Alex Carmack” для групп 5-го курса.

SELECT DISTINCT Subjects.Name FROM Teachers INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId INNER JOIN Subjects ON Lectures.SubjectId = Subjects.Id INNER JOIN GroupsLectures ON Lectures.Id = GroupsLectures.LectureId INNER JOIN `Groups` ON GroupsLectures.GroupId = `Groups`.Id WHERE Teachers.Name = "Alex" AND Teachers.Surname = "Carmack" AND `Groups`.Year = 5;

![текст](https://sun9-4.userapi.com/impg/0xfpl1tZ0nPiwSfMCuDvCLur46w1obF1yYqlug/QAIkFo7IRiI.jpg?size=1920x1080&quality=95&sign=c0c1d8d8920e988c505bb7ae9608471b&type=album)

4. Вывести фамилии преподавателей, которые не читают лекции по понедельникам.

SELECT DISTINCT Teachers.Surname FROM Teachers INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId LEFT JOIN Schedules ON Lectures.Id  = Schedules.LectureId AND Schedules.DayOfWeek = 1 WHERE Schedules.Id IS NULL;

![текст](https://sun9-4.userapi.com/impg/ouRwV2h1rI-IKiW_QmA96GXdPXuBecj83kYo2w/LJGJENfeehM.jpg?size=1920x1080&quality=95&sign=d62363a755e262bbc4487635553de5cc&type=album)

5. Вывести названия аудиторий, с указанием их корпусов, в которых нет лекций в среду второй недели на третьей паре.

SELECT DISTINCT CONCAT(LectureRooms.Name, ', ', LectureRooms.Building) FROM LectureRooms LEFT JOIN Schedules ON LectureRooms.Id = Schedules.LectureRoomId AND DayOfWeek = 3 AND Week = 2 AND Class = 3 WHERE Schedules.Id IS NULL;

![текст](https://sun9-77.userapi.com/impg/kNRVvupXafr57c0qxSRPRxOXkGpKrPG-cv1d4w/6NYpYnm0v-0.jpg?size=1920x1080&quality=95&sign=a6a094bb85f366aa2aa89f3126b5b1cd&type=album)

6. Вывести полные имена преподавателей факультета “Computer Science”, которые не курируют группы кафедры “Software Development”.

SELECT DISTINCT CONCAT(Teachers.Name, ' ', Teachers.Surname) FROM Teachers INNER JOIN Lectures ON Teachers.Id = Lectures.TeacherId INNER JOIN GroupsLectures ON Lectures.Id = GroupsLectures.LectureId INNER JOIN `Groups` AS Groups1 ON GroupsLectures.GroupId = Groups1.Id INNER JOIN Departments ON Groups1.DepartmentId = Departments.Id INNER JOIN Faculties ON Departments.FacultyId = Faculties.Id LEFT JOIN Curators ON Teachers.Id = Curators.TeacherId LEFT JOIN GroupsCurators ON Curators.Id = GroupsCurators.CuratorId LEFT JOIN `Groups` AS Groups2 ON GroupsCurators.GroupId = Groups2.Id AND Groups2.Name = "Software Development" WHERE Faculties.Name = "Computer Science" AND Groups2.Id IS NULL;

![текст](https://sun9-12.userapi.com/impg/M_8xLNXr5K2ooqsR8CFExV-7jsqKnnYNG5cvug/b-KRoW0KWS8.jpg?size=1920x1080&quality=95&sign=4d968194fb543e32826982928ebcfbe1&type=album)

7. Вывести список номеров всех корпусов, которые имеются в таблицах факультетов, кафедр и аудиторий.

SELECT Faculties.Building FROM Faculties UNION SELECT Departments.Building FROM Departments UNION SELECT LectureRooms.Building FROM LectureRooms;

![текст](https://sun9-21.userapi.com/impg/ivW7dpgAeM8wjfb-AQgnQ6ErwWDD75lsW1QpLg/sn3-6MFclAw.jpg?size=1920x1080&quality=95&sign=b46200ff9d1d4b88ad4430d6dfec1f98&type=album)

8. Вывести полные имена преподавателей в следующем порядке: деканы факультетов, заведующие кафедрами, преподаватели, кураторы, ассистенты.

SELECT CONCAT(Teachers.Name, ' ', Teachers.Surname) FROM Teachers INNER JOIN Deans ON Teachers.Id = Deans.TeacherId UNION SELECT CONCAT(Teachers.Name, ' ', Teachers.Surname) FROM Teachers INNER JOIN Departments ON Teachers.Id = Departments.HeadId UNION SELECT CONCAT(Teachers.Name, ' ', Teachers.Surname) FROM Teachers LEFT JOIN Deans ON Teachers.Id = Deans.TeacherId LEFT JOIN Departments ON Teachers.Id = Departments.HeadId LEFT JOIN Curators ON Teachers.Id = Curators.TeacherId LEFT JOIN Assistants ON Teachers.Id = Assistants.TeacherId WHERE Deans.Id IS NULL AND Departments.Id IS NULL AND Curators.Id IS NULL AND Assistants.Id IS NULL UNION SELECT CONCAT(Teachers.Name, ' ', Teachers.Surname) FROM Teachers INNER JOIN Curators ON Teachers.Id = Curators.TeacherId UNION SELECT CONCAT(Teachers.Name, ' ', Teachers.Surname) FROM Teachers INNER JOIN Assistants ON Teachers.Id = Assistants.TeacherId;

![текст](https://sun9-30.userapi.com/impg/34rVXBY5CfRJa3EK5l2VVK69TfD9N2Wz7_FWJw/LHlbjhYEiy4.jpg?size=1920x1080&quality=95&sign=cb02ce775a871e395d2bc3fb85285a8e&type=album)

9. Вывести дни недели (без повторений), в которые имеются занятия в аудиториях “A311” и “A104” корпуса 5. 

SELECT DISTINCT DayOfWeek FROM Schedules INNER JOIN LectureRooms ON Schedules.LectureRoomId = LectureRooms.Id WHERE Building = 5 AND (LectureRooms.Name = "A311" OR LectureRooms.Name = "A104");

![текст](https://sun9-38.userapi.com/impg/UvZtAZkPHX00jEUkGJfI7v2If3TNikd169gLFQ/P5yk8VzInxk.jpg?size=1920x1080&quality=95&sign=5d5cab3bdafd56ca4baf7e606629ec18&type=album) 