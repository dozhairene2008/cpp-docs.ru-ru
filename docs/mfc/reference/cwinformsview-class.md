---
title: Класс Квинформсвиев
ms.date: 11/04/2016
f1_keywords:
- CWinFormsView
- AFXWINFORMS/CWinFormsView
- AFXWINFORMS/CWinFormsView::CWinFormsView
- AFXWINFORMS/CWinFormsView::GetControl
helpviewer_keywords:
- CWinFormsView [MFC], CWinFormsView
- CWinFormsView [MFC], GetControl
ms.assetid: d597e397-6529-469b-88f5-7f65a6b9e895
ms.openlocfilehash: f4a5e6b88527dad8606092ccebd4899bba5181f6
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79426291"
---
# <a name="cwinformsview-class"></a>Класс Квинформсвиев

Предоставляет универсальную функцию для размещения элементов управления Windows Forms в качестве представления MFC.

## <a name="syntax"></a>Синтаксис

```
class CWinFormsView : public CView;
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|Имя|Description|
|----------|-----------------|
|[Квинформсвиев:: Квинформсвиев](#cwinformsview)|Формирует объект `CWinFormsView`.|

### <a name="public-methods"></a>Открытые методы

|Имя|Description|
|----------|-----------------|
|[Квинформсвиев:: oncontrol](#getcontrol)|Извлекает указатель на элемент управления Windows Forms.|

### <a name="public-operators"></a>Открытые операторы

|Имя||
|----------|-|
|[Квинформсвиев:: operator элемент управления ^](#operator_control)|Приводит тип в качестве указателя на элемент управления Windows Forms.|

## <a name="remarks"></a>Remarks

MFC использует класс `CWinFormsView` для размещения элемента управления Windows Forms .NET Framework в представлении MFC. Элемент управления является дочерним для собственного представления и занимает всю клиентскую область представления MFC. Результат аналогичен представлению `CFormView`, что позволяет использовать преимущества конструктора Windows Forms и времени выполнения для создания расширенных представлений на основе форм.

Дополнительные сведения об использовании Windows Forms см. в разделе [Использование пользовательского элемента управления формы Windows в MFC](../../dotnet/using-a-windows-form-user-control-in-mfc.md).

> [!NOTE]
>  Интеграция с MFC Windows Forms работает только в проектах, которые динамически связываются с MFC (проектами, в которых определен AFXDLL).

> [!NOTE]
>  Квинформсвиев не поддерживает окно разделителя MFC ( [класс CSplitterWnd](../../mfc/reference/csplitterwnd-class.md)). В настоящее время поддерживается только элемент управления "разделитель Windows Forms".

## <a name="requirements"></a>Требования

**Заголовок:** афксвинформс. h

##  <a name="cwinformsview"></a>Квинформсвиев:: Квинформсвиев

Формирует объект `CWinFormsView`.

```
CWinFormsView(System::Type^ pManagedViewType);
```

### <a name="parameters"></a>Параметры

*пманажедвиевтипе*<br/>
Указатель на тип данных Windows Forms пользовательского элемента управления.

### <a name="example"></a>Пример

В следующем примере класс `CUserView` наследует от `CWinFormsView` и передает тип `UserControl1` в конструктор `CWinFormsView`. `UserControl1` является пользовательским элементом управления в ControlLibrary1. dll.

[!code-cpp[NVC_MFC_Managed#1](../../mfc/reference/codesnippet/cpp/cwinformsview-class_1.h)]

[!code-cpp[NVC_MFC_Managed#2](../../mfc/reference/codesnippet/cpp/cwinformsview-class_2.cpp)]

##  <a name="getcontrol"></a>Квинформсвиев:: oncontrol

Извлекает указатель на элемент управления Windows Forms.

```
System::Windows::Forms::Control^ GetControl() const;
```

### <a name="return-value"></a>Возвращаемое значение

Указатель на объект `System.Windows.Forms.Control`.

### <a name="remarks"></a>Remarks

Пример использования Windows Forms см. [в разделе Использование пользовательского элемента управления формы Windows в MFC](../../dotnet/using-a-windows-form-user-control-in-mfc.md).

##  <a name="operator_control"></a>Квинформсвиев:: operator элемент управления ^

Приводит тип в качестве указателя на элемент управления Windows Forms.

```
operator System::Windows::Forms::Control^() const;
```

### <a name="remarks"></a>Remarks

Этот оператор позволяет передать `CWinFormsView` представление функциям, которые принимают указатель на Windows Forms элемент управления типа <xref:System.Windows.Forms.Control>.

### <a name="example"></a>Пример

  См. раздел [квинформсвиев:: oncontrol](#getcontrol).

## <a name="see-also"></a>См. также раздел

[Диаграмма иерархии](../../mfc/hierarchy-chart.md)<br/>
[Класс CWinFormsControl](../../mfc/reference/cwinformscontrol-class.md)<br/>
[Класс CWinFormsDialog](../../mfc/reference/cwinformsdialog-class.md)<br/>
[Класс CFormView](../../mfc/reference/cformview-class.md)
