## Подготовка данных сотрудников
{{% section %}}

### Ручки

---

    {{% note %}}
    - Раз в час, ходим по ручкам,
    - получаем актуальные данные по всем сотрудникам, 
    - берем текущие из таблички employees, 
    - делаем словари,
    - перебираем массив актуальных данных, 
    - сравниваем с текущими, 
    - сли есть изменения записываем их в таблички, 
    - помечаем их как необработанные.
    {{% /note %}}

![](/images/data/diagrams/staff-core/FillChangesFlowHandlers.svg)

---

    {{% note %}}
    Топик информации по сотрам - 
    вычитали событие,
    записали его в EmployeeChangesRaw
    сходили в БД проверили предыдущее состояние в EmployeeLastChangesRaw
    если предыдущего состояния нет - создаем новое где prevData - пусто, а data текущее состояние
    если предыдущее состояние есть - создаем новое где prevData это data предыдущего состояния, а data это новое текущиее состояние
    - плюс такого решения - не нужно агрегировать много ченджей, достаточно взять его один раз lastchanges
    - chages_raw вцелом больше просто историческая табличка для быстрого разбора ситуаций
    {{% /note %}}

### Топик информации по сотрам

---

    {{% note %}}
    Топик Аккаунтов:
    работает как емплои ченджс
    {{% /note %}}

### Топик Аккаунтов

---

    {{% note %}}
    Топик приказов читается а затем пишется пишется в employee_hire_changes_raw 
    {{% /note %}}

### Топик приказов на найм/увольнение

---

    {{% note %}}
    Топик грейдов:
    слушаем кафку, 
    по прилету события вставляем строку в raw, 
    смотрим был ли у нас такой документ, 
    если пришла новая версия - обновляем в таблице актуальных грейдов данные, 
    ыудаляем если пришла отмена или его распровели
    {{% /note %}}

### Топик приказов на изменение грейда

{{% /section %}}