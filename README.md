# sFuncName
Func _WD_WaitElement($sSession, $sStrategy, $sSelector, $sStartElement = "", $lMultiple = False, $iDelay = 0, $iTimeout = -1)     Local Const $sFuncName = "_WD_WaitElement"     Local $bAbort = False, $iErr, $iResult      If $iTimeout = -1 Then $iTimeout = $_WD_DefaultTimeout      Sleep($iDelay)      Local $hWaitTimer = TimerInit()      While 1         $FindRet = _WD_FindElement($sSession, $sStrategy, $sSelector, $sStartElement, $lMultiple)         $iErr = @error          If $iErr = $_WD_ERROR_Success Then             $iResult = 1             ExitLoop          ElseIf $iErr = $_WD_ERROR_NoMatch Then             If (TimerDiff($hWaitTimer) > $iTimeout) Then                 $iErr = $_WD_ERROR_Timeout                 ExitLoop             EndIf         Else             ExitLoop         EndIf          Sleep(1000)     WEnd      Return SetError(__WD_Error($sFuncName, $iErr), $iResult, $FindRet) EndFunc
