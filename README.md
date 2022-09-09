# Mozilla Firefox Core 104.0.2 - 'Graphics WebRender' Zero-Click-Remote-Denial-of-Service
#The attacker can do a successful Denial of Service by sending a link to the target and without the target clicking on a specific link. #crash from PWebRenderBridgeChild::SendSetDisplayList while loading a PDF

![alt text](https://github.com/APTIRAN/Mozilla-Firefox-Core-104.0.2-Graphics-WebRender-Zero-Click-Remote-Denial-of-Service/blob/main/GIF/POC.gif)

<code>
xul.dll!mozilla::ipc::PortLink::SendMessage(mozilla::UniquePtr<IPC::Message,mozilla::DefaultDelete<IPC::Message>> aMessage) Line 95	C++
 	xul.dll!mozilla::ipc::MessageChannel::SendMessageToLink(mozilla::UniquePtr<IPC::Message,mozilla::DefaultDelete<IPC::Message>> aMsg) Line 783	C++
 	xul.dll!mozilla::ipc::MessageChannel::Send(mozilla::UniquePtr<IPC::Message,mozilla::DefaultDelete<IPC::Message>> aMsg) Line 772	C++
 	xul.dll!mozilla::ipc::IProtocol::ChannelSend(mozilla::UniquePtr<IPC::Message,mozilla::DefaultDelete<IPC::Message>> aMsg) Line 493	C++
 	xul.dll!mozilla::layers::PWebRenderBridgeChild::SendSetDisplayList(mozilla::layers::DisplayListData && displayList, const nsTArray<mozilla::layers::OpDestroy> & toDestroy, const unsigned __int64 & fwdTransactionId, const mozilla::layers::BaseTransactionId<mozilla::layers::TransactionIdType> & transactionId, const bool & containsSVGGroup, const mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> & vsyncId, const mozilla::TimeStamp & vsyncStartTime, const mozilla::TimeStamp & refreshStartTime, const mozilla::TimeStamp & txnStartTime, const nsTString<char> & txnURL, const mozilla::TimeStamp & fwdTime, const nsTArray<mozilla::layers::CompositionPayload> & payloads) Line 311	C++
 	xul.dll!mozilla::layers::WebRenderBridgeChild::EndTransaction(mozilla::layers::DisplayListData && aDisplayListData, mozilla::layers::BaseTransactionId<mozilla::layers::TransactionIdType> aTransactionId, bool aContainsSVGGroup, const mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> & aVsyncId, const mozilla::TimeStamp & aVsyncStartTime, const mozilla::TimeStamp & aRefreshStartTime, const mozilla::TimeStamp & aTxnStartTime, const nsTString<char> & aTxnURL) Line 127	C++
 	xul.dll!mozilla::layers::WebRenderLayerManager::EndTransactionWithoutLayer(mozilla::nsDisplayList * aDisplayList, mozilla::nsDisplayListBuilder * aDisplayListBuilder, WrFiltersHolder && aFilters, mozilla::layers::WebRenderBackgroundData * aBackground, const double aGeckoDLBuildTime) Line 463	C++
 	xul.dll!mozilla::nsDisplayList::PaintRoot(mozilla::nsDisplayListBuilder * aBuilder, gfxContext * aCtx, unsigned int aFlags, mozilla::Maybe<double> aDisplayListBuildTime) Line 2306	C++
 	xul.dll!nsLayoutUtils::PaintFrame(gfxContext * aRenderingContext, nsIFrame * aFrame, const nsRegion & aDirtyRegion, unsigned int aBackstop, mozilla::nsDisplayListBuilderMode aBuilderMode, nsLayoutUtils::PaintFrameFlags aFlags) Line 3456	C++
 	xul.dll!mozilla::PresShell::PaintInternal(nsView * aViewToPaint, mozilla::PaintInternalFlags aFlags) Line 6433	C++
 	xul.dll!nsViewManager::ProcessPendingUpdatesPaint(nsIWidget * aWidget) Line 441	C++
 	xul.dll!nsViewManager::ProcessPendingUpdatesForView(nsView * aView, bool aFlushDirtyRegion) Line 376	C++
 	xul.dll!nsViewManager::ProcessPendingUpdates() Line 949	C++
 	xul.dll!nsRefreshDriver::Tick(mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> aId, mozilla::TimeStamp aNowTime, nsRefreshDriver::IsExtraTick aIsExtraTick) Line 2730	C++
 	[Inline Frame] xul.dll!mozilla::RefreshDriverTimer::TickDriver(nsRefreshDriver * driver, mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> aId, mozilla::TimeStamp) Line 375	C++
 	xul.dll!mozilla::RefreshDriverTimer::TickRefreshDrivers(mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> aId, mozilla::TimeStamp aNow, nsTArray<RefPtr<nsRefreshDriver>> & aDrivers) Line 353	C++
 	xul.dll!mozilla::RefreshDriverTimer::Tick(mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> aId, mozilla::TimeStamp now) Line 371	C++
 	xul.dll!mozilla::VsyncRefreshDriverTimer::RunRefreshDrivers(mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> aId, mozilla::TimeStamp aTimeStamp) Line 897	C++
 	xul.dll!mozilla::VsyncRefreshDriverTimer::TickRefreshDriver(mozilla::layers::BaseTransactionId<mozilla::VsyncIdType> aId, mozilla::TimeStamp aVsyncTimestamp) Line 810	C++
 	xul.dll!mozilla::VsyncRefreshDriverTimer::NotifyVsyncOnMainThread(const mozilla::VsyncEvent & aVsyncEvent) Line 732	C++
 	xul.dll!mozilla::VsyncRefreshDriverTimer::RefreshDriverVsyncObserver::NotifyVsyncTimerOnMainThread() Line 595	C++
 	[Inline Frame] xul.dll!mozilla::VsyncRefreshDriverTimer::RefreshDriverVsyncObserver::NotifyVsync::<lambda_1>::operator()() Line 566	C++
 	xul.dll!mozilla::detail::RunnableFunction<`lambda at C:/dev/mozilla-unified/layout/base/nsRefreshDriver.cpp:565:15'>::Run() Line 532	C++
 	xul.dll!mozilla::RunnableTask::Run() Line 539	C++
 	xul.dll!mozilla::TaskController::DoExecuteNextTaskOnlyMainThreadInternal(const mozilla::detail::BaseAutoLock<mozilla::Mutex &> & aProofOfLock) Line 851	C++
 	xul.dll!mozilla::TaskController::ExecuteNextTaskOnlyMainThreadInternal(const mozilla::detail::BaseAutoLock<mozilla::Mutex &> & aProofOfLock) Line 683	C++
 	xul.dll!mozilla::TaskController::ProcessPendingMTTask(bool aMayWait) Line 461	C++
 	[Inline Frame] xul.dll!mozilla::TaskController::InitializeInternal::<lambda_1>::operator()() Line 187	C++
 	xul.dll!mozilla::detail::RunnableFunction<`lambda at C:/dev/mozilla-unified/xpcom/threads/TaskController.cpp:187:7'>::Run() Line 532	C++
 	xul.dll!nsThread::ProcessNextEvent(bool aMayWait, bool * aResult) Line 1209	C++
 	xul.dll!NS_ProcessNextEvent(nsIThread * aThread, bool aMayWait) Line 465	C++
 	xul.dll!mozilla::ipc::MessagePump::Run(base::MessagePump::Delegate * aDelegate) Line 86	C++
 	[Inline Frame] xul.dll!MessageLoop::RunInternal() Line 380	C++
 	xul.dll!MessageLoop::RunHandler() Line 374	C++
 	xul.dll!MessageLoop::Run() Line 356	C++
 	xul.dll!nsBaseAppShell::Run() Line 152	C++
 	xul.dll!nsAppShell::Run() Line 613	C++
 	xul.dll!nsAppStartup::Run() Line 296	C++
 	xul.dll!XREMain::XRE_mainRun() Line 5748	C++
 	xul.dll!XREMain::XRE_main(int argc, char * * argv, const mozilla::BootstrapConfig & aConfig) Line 5942	C++
 	xul.dll!XRE_main(int argc, char * * argv, const mozilla::BootstrapConfig & aConfig) Line 6006	C++
 	[Inline Frame] firefox.exe!do_main(int argc, char * * argv, char * * envp) Line 227	C++
 	firefox.exe!NS_internal_main(int argc, char * * argv, char * * envp) Line 406	C++
 	firefox.exe!wmain(int argc, wchar_t * * argv) Line 167	C++
</code>

