<template>
  <div>
    <h1>System Log Reading (Simulated)</h1>
    <button @click="iniciarLectura">Start Reading Logs</button>
    <div class="logs">
      <div v-for="(log, index) in logs" :key="index">
        {{ log }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LogViewer',
  data() {
    return {
      logs: [],
      simulatedLogs: [
        "Jan 01 00:00:01 systemd[1]: Started Session 1 of user root.",
        "Jan 01 00:00:02 kernel: [0.000000] Linux version 5.4.0 (gcc version 9.3.0)",
        "Jan 01 00:00:03 sshd[1234]: Accepted password for user from 192.168.1.100 port 22 ssh2",
        "Jan 01 00:00:04 CRON[2345]: (root) CMD (some cron job)",
        "Jan 01 00:00:05 kernel: [0.000001] PCI: Using ACPI for IRQ routing"
      ],
      intervalId: null,
      logIndex: 0
    }
  },
  methods: {
    iniciarLectura() {
      this.logs = [];
      this.logIndex = 0;
      if (this.intervalId) clearInterval(this.intervalId);
      this.intervalId = setInterval(() => {
        if (this.logIndex < this.simulatedLogs.length) {
          this.logs.push(this.simulatedLogs[this.logIndex]);
          this.logIndex++;
        } else {
          clearInterval(this.intervalId);
        }
      }, 1000);
    }
  },
  beforeDestroy() {
    if (this.intervalId) clearInterval(this.intervalId);
  }
}
</script>

<style scoped>
.logs {
  background-color: #1e1e1e;
  color: #00ff00;
  padding: 10px;
  height: 200px;
  overflow-y: auto;
  font-family: monospace;
  border: 1px solid #333;
}
</style>