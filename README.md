# clsMQTT
VB.Net code for MQTTnet 3.0.* library
https://github.com/dotnet/MQTTnet

    Private WithEvents mqtt As clsMQTT

    Private Sub mqttStart()
        mqtt = New clsMQTT
        mqtt.Create(BrokerIP, BrokerPort, BrokerUser, BrokerPass)
        mqtt.Connect.Wait(1000)
        If mqtt.IsConnected Then
            ' mqtt.Subscribe(Topic).Wait(1000)
        Else
            mqtt = New clsMQTT 'simple way to stop my library completely
        End If
    End Sub

    Private Sub Received(Topic As String, Payload As String) Handles mqtt.Recieved
        	
    End Sub

    Public Sub mqttReconnect()
        mqtt.Reconnect.Wait(1000)
        If mqtt.IsConnected Then
           ' mqtt.Unsubscribe(Topics).Wait(1000) 
           ' mqttSubscribeAdd(Topic)
        End If
    End Sub

    Public Sub mqttSubscribeAdd(Topic As String)
        If mqtt.IsConnected Then
            ' mqtt.Subscribe(Topic).Wait(1000)
        End If
    End Sub

    Public Sub mqttSubscribeRemove(Topics As String())
        If mqtt.IsConnected Then
            ' mqtt.Unsubscribe(Topics).Wait(1000)
        End If
    End Sub

    Private Sub Err(Message As String, Task As clsMQTT.TaskErr) Handles mqtt.Err
        Dispatcher.Invoke(Sub() ShowMessage(Message, Task))
    End Sub

    Private Sub ShowMessage(Message As String, Task As clsMQTT.TaskErr)
	  If Task = clsMQTT.TaskErr.Disconnect Then
            mqtt = New clsMQTT 
        Else
            If mqtt IsNot Nothing AndAlso mqtt.IsConnected Then mqtt.Disconnect.Wait() 'due to multiple errors is better to disconnect
            MessageBox.Show(Message, "MQTT Client", MessageBoxButton.OK, MessageBoxImage.Error)
        End If
    End Sub

I would like to pass on my experience in VB.Net to others and thus support this language for future generations. There are difficult beginnings in any programming language, when you have to learn to use new language libraries so that you can take even the smallest step. I want to help you with that now. You're welcome, signed Zdeněk Jantač.
