---
title: Класс CMFCDragFrameImpl
ms.date: 10/18/2018
f1_keywords:
- CMFCDragFrameImpl
helpviewer_keywords:
- CMFCDragFrameImpl class [MFC]
ms.assetid: 500cd824-8188-43c2-8754-b7bb46b5648a
ms.openlocfilehash: 05b4426da6bee0443a407cff583f47bee60262e4
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62348618"
---
# <a name="cmfcdragframeimpl-class"></a>Класс CMFCDragFrameImpl

`CMFCDragFrameImpl` Класс рисует прямоугольник перетаскивания, который появляется, когда пользователь перетаскивает область в стандартном режиме закрепления.
Дополнительные сведения см. в исходном коде, расположенном в папке **VC\\atlmfc\\src\\mfc** каталога установки Visual Studio.

## <a name="syntax"></a>Синтаксис

```
class CMFCDragFrameImpl
```

## <a name="remarks"></a>Примечания

Объект этого класса внедряется в каждом [класс CPane](../../mfc/reference/cpane-class.md) объекта. Таким образом, для каждой области, который использует `CanFloat` метод отображает прямоугольника перетаскивания, когда пользователь перетаскивает его.

Ширина прямоугольника перетаскивания можно управлять с помощью [AFX_GLOBAL_DATA::m_nDragFrameThicknessFloat](afx-global-data-structure.md#m_ndragframethicknessfloat) и [AFX_GLOBAL_DATA::m_nDragFrameThicknessDock](afx-global-data-structure.md#m_ndragframethicknessdock).

## <a name="inheritance-hierarchy"></a>Иерархия наследования

[CMFCDragFrameImpl](../../mfc/reference/cmfcdragframeimpl-class.md)

## <a name="requirements"></a>Требования

**Заголовок:** afxdragframeimpl.h

##  <a name="enddrawdragframe"></a>  CMFCDragFrameImpl::EndDrawDragFrame

```
void EndDrawDragFrame(BOOL bClearInternalRects = TRUE);
```

### <a name="parameters"></a>Параметры

[in] *bClearInternalRects*<br/>

### <a name="remarks"></a>Примечания

##  <a name="init"></a>  CMFCDragFrameImpl::Init

```
void Init(CWnd* pDraggedWnd);
```

### <a name="parameters"></a>Параметры

[in] *pDraggedWnd*<br/>

### <a name="remarks"></a>Примечания

##  <a name="movedragframe"></a>  CMFCDragFrameImpl::MoveDragFrame

```
void MoveDragFrame(BOOL bForceMove = FALSE);
```

### <a name="parameters"></a>Параметры

[in] *bForceMove*<br/>

### <a name="remarks"></a>Примечания

##  <a name="placetabpredocking"></a>  CMFCDragFrameImpl::PlaceTabPreDocking

```
void PlaceTabPreDocking(
    CBaseTabbedPane* pTabbedBar,
    BOOL bFirstTime);

void PlaceTabPreDocking(CWnd* pCBarToPlaceOn);
```

### <a name="parameters"></a>Параметры

[in] *pTabbedBar*<br/>

[in] *bFirstTime*<br/>

[in] *pCBarToPlaceOn*<br/>

### <a name="remarks"></a>Примечания

##  <a name="removetabpredocking"></a>  CMFCDragFrameImpl::RemoveTabPreDocking

```
void RemoveTabPreDocking(CDockablePane* pOldTargetBar = NULL);
```

### <a name="parameters"></a>Параметры

[in] *pOldTargetBar*<br/>

### <a name="remarks"></a>Примечания

##  <a name="resetstate"></a>  CMFCDragFrameImpl::ResetState

```
void ResetState();
```

### <a name="remarks"></a>Примечания

## <a name="see-also"></a>См. также

[Диаграмма иерархии](../../mfc/hierarchy-chart.md)<br/>
[Классы](../../mfc/reference/mfc-classes.md)<br/>
[Класс CPane](../../mfc/reference/cpane-class.md)
