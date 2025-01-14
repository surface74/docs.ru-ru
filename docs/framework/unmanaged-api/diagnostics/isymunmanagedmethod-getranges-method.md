---
title: Метод ISymUnmanagedMethod::GetRanges
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetRanges
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetRanges
helpviewer_keywords:
- ISymUnmanagedMethod::GetRanges method [.NET Framework debugging]
- GetRanges method [.NET Framework debugging]
ms.assetid: a85283d8-379c-417a-9736-ddeeef9bcf50
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ef5a98d510eee8942a2cad0525b6902e3e4eaa52
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769387"
---
# <a name="isymunmanagedmethodgetranges-method"></a>Метод ISymUnmanagedMethod::GetRanges
Возвращает массив пар начального и конечного смещения, соответствующих диапазонам на языке MSIL, занимаемым позиция в этом методе обозначение позиции в документе. Массив представляет собой массив целых чисел и имеет формат [начало, конец, начало, конец]. Число пар "диапазон" — Длина массива, поделенную на 2.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT GetRanges(  
    [in]  ISymUnmanagedDocument* document,  
    [in]  ULONG32                line,  
    [in]  ULONG32                column,  
    [in]  ULONG32                cRanges,  
    [out] ULONG32                *pcRanges,  
    [out, size_is(cRanges),  
        length_is(*pcRanges)] ULONG32 ranges[]);  
```  
  
## <a name="parameters"></a>Параметры  
 `document`  
 [in] Документ, для которого запрашивается смещение.  
  
 `line`  
 [in] Строка документа, соответствующая этим диапазонам.  
  
 `column`  
 [in] Столбец документа, соответствующая этим диапазонам.  
  
 `cRanges`  
 [in] Размер массива `ranges`.  
  
 `pcRanges`  
 [out] Указатель на `ULONG32` , получающий размер буфера, необходимый для диапазонов.  
  
 `ranges`  
 [out] Указатель на буфер, получающий диапазоны.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Значение S_OK, если метод выполнен успешно; в противном случае — значение E_FAIL или другим кодом ошибки.  
  
## <a name="requirements"></a>Требования  
 **Заголовок.** CorSym.idl CorSym.h  
  
## <a name="see-also"></a>См. также

- [Интерфейс ISymUnmanagedMethod](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedmethod-interface.md)
