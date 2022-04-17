# Change Log

* Increase maximum time scale for plotted waveforms ([#1][pr-1])
    * Added 10000 ms, 20000 ms, and 40000 ms.

* Increase maximum phase durations in stimulation dialog window ([#2][pr-2])
    * First and second phase durations were capped at 5 ms each. These were
      increased to allow for the longest possible pulses permitted by the
      hardware (~2-3 seconds, depending on sampling period). The sum of the
      post-trigger delay, the post-stim refractory period, and the total
      duration of the multiphasic waveform (first and second phases plus
      interphase delay, depending on the stimulation shape) cannot exceed this
      maximum pulse duration.

[pr-1]: https://github.com/CWRUChielLab/Intan-RHX/pull/1
[pr-2]: https://github.com/CWRUChielLab/Intan-RHX/pull/2
